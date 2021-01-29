<template>
  <main>
    <h2>Welcome {{ userName }}</h2>
    <h1>This is your Dashboard.</h1>
    <NuxtLink to="/">
      Back home
    </NuxtLink>
    <div class="container" v-if="ads">
      <ul v-for="ad of ads" :key="ad._id">
        <li>{{ ad.text }}</li>
        <li>{{ ad.url }}</li>
        <li>{{ ad.user }}</li>
        <button class="bg-red-500 text-white active:bg-blue-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1" @click="deleteAd(ad._id)">Supprimer</button>
        <ComponentUpdateAdModal buttonText="Editer" :ad="ad" @updatingAd="updateAd"/>
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
import ComponentUpdateAdModal from '../components/ComponentUpdateAdModal.vue';
export default {
  components: { ComponentUpdateAdModal },
  middleware: 'authenticated',
  data() {
    return {
      ads: null,
      text: null,
      image: null,
      url: null,
      userName: null,
      userEmail: null
    }
  },
  beforeMount(){
    this.getAds();
    this.userName = this.$store.state.user.name;
    this.userEmail = this.$store.state.user.email;
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
          if (res.authenticated) {
            this.$router.push('/login')
          }
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
    },
    deleteAd(item){
      const options = {
        method: 'DELETE',
        body: JSON.stringify(item),
        headers: {
          Authorization: `Bearer: ${this.$store.state.auth.accessToken.Token}`,
          'Content-Type': 'application/json'
        }
      }
      fetch('http://localhost:5000/api/ads', options);
      this.getAds();
    },
    updateAd(item){
        console.log({item});
        const options = {
        method: 'PUT',
        body: JSON.stringify(item),
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
