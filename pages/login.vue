<template>
  <div class="h-screen flex flex-col">
    <componentNavbar />
    <componentLogin @logingUser="postLogin" :message="message"/>
  </div>
</template>

<script>
const Cookie = process.client ? require('js-cookie') : undefined;
import ComponentNavbar from '../components/ComponentNavbar.vue';
import ComponentLogin from '../components/ComponentLogin.vue';

export default {
  components: { ComponentLogin, ComponentNavbar },
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
    postLogin(user) {
      console.log({user});
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
                  this.$router.push('/dashboard');
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
