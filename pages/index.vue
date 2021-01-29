<template>
    <div>
        <componentNavbar />
    </div>
</template>

<script>
const Cookie = process.client ? require('js-cookie') : undefined
import ComponentNavbar from '../components/ComponentNavbar.vue';

export default {
  components: { ComponentNavbar },
  methods: {
    logout2 () {
      Cookie.remove('auth')
      this.$store.commit('setAuth', null)
    }
  }
}
</script>
