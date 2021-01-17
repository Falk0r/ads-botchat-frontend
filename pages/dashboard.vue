<template>
  <main>
    <h1>This is dashboard page.</h1>
    <NuxtLink to="/">
      Back home
    </NuxtLink>
    <div class="container" v-if="ads">
      <ul v-for="ad of ads" :key="ad._id">
        <li>{{ ad.text }}</li>
        <li>{{ ad.url }}</li>
        <li>{{ ad.user }}</li>
      </ul>
    </div>
    <div class="container">
      <label for="text">
        <input id="text" type="text" v-model="text" placeholder="text">
      </label>
      <label for="image">
        <input id="image" type="" v-model="image" placeholder="image">
      </label>
      <label for="url">
        <input id="url" type="url" v-model="url" placeholder="url">
      </label>
      <button @click="createAd">
        Créer
      </button>
    </div>
  </main>
</template>

<script>
export default {
  middleware: 'authenticated',
  data() {
    return {
      ads: null,
      text: null,
      image: null,
      url: null
    }
  },
  beforeMount(){
    this.getAds();
  },
  methods: {
    getAds() {
      const options = {
        method: 'GET',
        headers: {
          Authorization: `Bearer: ${this.$store.state.auth.accessToken.Token}`
        }
      }
      fetch('http://localhost:5000/api/ads', options)
        .then(res => res.json())
        .then(res => {
          console.log(res);
          this.ads = res;
        })
    },
    createAd() {
      const ad = {
        'text' : this.text,
        'image' : this.image,
        'url' : this.url
      }
      const options = {
        method: 'POST',
        body: JSON.stringify(ad),
        headers: {
          Authorization: `Bearer: ${this.$store.state.auth.accessToken.Token}`,
          'Content-Type': 'application/json'
        }
      }
      fetch('http://localhost:5000/api/ads', options);
      this.getAds();
    }
  }
}
</script>
