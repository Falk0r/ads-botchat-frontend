<template>
  <main>
    <ComponentNavbar @creatingAd="createAd"/>
    <div v-if="ads" class="flex flex-wrap justify-around space-x-1 space-y-1">
      <div v-for="ad of ads" :key="ad._id">
        <ComponentDashboardCard :ad="ad" @updatingAd="updateAd" @deletingAd="deleteAd" @publishingAd="publishAd" />
      </div>
    </div>
  </main>
</template>

<script>
import ComponentNavbar from '../components/ComponentNavbar.vue';
import ComponentUpdateAdModal from '../components/ComponentUpdateAdModal.vue';
import ComponentDashboardCard from '../components/ComponentDashboardCard.vue';
export default {
  components: { ComponentUpdateAdModal, ComponentNavbar, ComponentDashboardCard },
  middleware: 'authenticated',
  data() {
    return {
      ads: null,
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
    createAd(item) {
      const ad = {
        'text' : this.text,
        'image' : this.image,
        'url' : this.url,
        'title' : this.title
      }
      const options = {
        method: 'POST',
        body: JSON.stringify(item),
        headers: {
          Authorization: `Bearer: ${this.$store.state.auth.accessToken.Token}`,
          'Content-Type': 'application/json'
        }
      }
      fetch('http://localhost:5000/api/ads', options)
        .then(this.getAds());
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
      fetch('http://localhost:5000/api/ads', options)
        .then(this.getAds());
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
      fetch('http://localhost:5000/api/ads', options)
        .then(this.getAds());
    },
    publishAd(item){
      console.log({item});
      let url;
      if (item.status === "publish") {
        url = 'http://127.0.0.1:5000/publish';        
      } else {
        url = 'http://127.0.0.1:5000/depublish';
      }
      const options = {
        method: 'POST',
        body: JSON.stringify(item),
        headers: {
          Authorization: `Bearer: ${this.$store.state.auth.accessToken.Token}`,
          'Content-Type': 'application/json'
        }
      }
      console.log(url);
      fetch(url, options)
        .then(res => res.json())
        .then(res => {
          console.log(res);
        })
        .then(this.getAds());
    }
  }
}
</script>
