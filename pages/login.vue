<template>
  <div class="container">
    <h1>Sign in to access to your Dashboard</h1>
    <div>
      <label for="name">
        <input id="name" type="name" value="test" v-model="name" placeholder="name">
      </label>
      <label for="email">
        <input id="email" type="email" value="test" v-model="email" placeholder="email">
      </label>
      <label for="password">
        <input id="password" type="password" value="test" v-model="password" placeholder="password">
      </label>
      <button @click="postLogin">
        Login
      </button>
    </div>
    <h3>{{message}}</h3>
  </div>
</template>

<script>
const Cookie = process.client ? require('js-cookie') : undefined

export default {
  middleware: 'notAuthenticated',
  data() {
      return {
          name: null,
          email: null,
          password: null,
          message: null
      }
  },
  methods: {
    postLogin () {
        const user = {
            'name': this.name,
            'email': this.email,
            'password': this.password
        }
        const options = {
            method: 'POST',
            body: JSON.stringify(user),
            headers: {
                'Content-Type': 'application/json'
            }
        }
        fetch('http://localhost:5000/login', options)
            .then(res => res.json())
            .then(res => {
                console.log(res);
                if (res.authenticated) {
                  const auth = {
                  accessToken: res
                  }
                  this.decodePayload(res.Token);
                  this.$store.commit('setAuth', auth) // mutating to store for client rendering
                  Cookie.set('auth', auth) // saving token in cookie for server rendering
                  this.$router.push('/dashboard')
                } else {
                  this.message = res.Message;
                }
            })
    },
    decodePayload(token){
      const payload = JSON.parse(atob(token.split('.')[1]));
      this.$store.commit('setPayload', payload);
    }
  }
}
</script>
