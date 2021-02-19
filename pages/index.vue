<template>
    <div class="leading-normal tracking-normal text-white gradient">
        <componentNavbar />
        <callToAction />
        <component-wave-home />
        <component-section-one />
        <component-section-two />
        <component-section-prices />
        <component-wave-bottom-home />
        <component-call-to-action-bottom />
    </div>
</template>

<script>
const Cookie = process.client ? require('js-cookie') : undefined
import ComponentNavbar from '../components/ComponentNavbar.vue';
import callToAction from '../components/ComponentCalltoActionHome.vue';
import ComponentWaveHome from '../components/ComponentWaveHome.vue';
import ComponentSectionOne from '../components/ComponentSectionOne.vue';
import ComponentSectionTwo from '../components/ComponentSectionTwo.vue';
import ComponentSectionPrices from '../components/ComponentSectionPrices.vue';
import ComponentWaveBottomHome from '../components/ComponentWaveBottomHome.vue';
import ComponentCallToActionBottom from '../components/ComponentCallToActionBottom.vue';

export default {
  components: { ComponentNavbar,callToAction, ComponentWaveHome, ComponentSectionOne, ComponentSectionTwo, ComponentSectionPrices, ComponentWaveBottomHome },
  methods: {
    logout2 () {
      Cookie.remove,
    ComponentCallToActionBottom('auth')
      this.$store.commit('setAuth', null)
    }
  }
}
</script>
<style>
      .gradient {
        background: linear-gradient(90deg, #d53369 0%, #daae51 100%);
      }
</style>
