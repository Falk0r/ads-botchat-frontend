<template>
    <div>
        <button class="bg-white text-red-500 px-4 py-2 rounded mr-auto hover:underline" type="button" style="transition: all .15s ease" v-on:click="toggleModal()">
        {{buttonText}}
        </button>
        <div v-if="showModal" class="overflow-x-hidden overflow-y-auto fixed inset-0 z-50 outline-none focus:outline-none justify-center items-center flex">
            <div class="relative py-3 sm:max-w-xl sm:mx-auto">
                <div class="relative px-4 py-10 bg-white mx-8 md:mx-0 shadow rounded-3xl sm:p-10">
                    <div class="max-w-md mx-auto">
                        <div class="flex items-center space-x-5">
                            <div class="h-14 w-14 bg-red-200 rounded-full flex flex-shrink-0 justify-center items-center text-red-500 text-2xl font-mono">S</div>
                            <div class="block pl-2 font-semibold text-xl self-start text-gray-700">
                                <h2 class="leading-relaxed">Supprimer la Pub</h2>
                                <p class="text-sm text-gray-500 font-normal leading-relaxed">Veux-tu vraiment supprimer ta pub ?</p>
                            </div>
                        </div>
                        <div class="divide-y divide-gray-200">
                        <div class="py-8 text-base leading-6 space-y-4 text-gray-700 sm:text-lg sm:leading-7">
                            <div class="flex flex-col">
                            <label class="leading-loose">Titre</label>
                            <p class="px-4 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600">{{adToDelete.title}}</p>
                            </div>
                        </div>
                        <div class="pt-4 flex items-center space-x-4">
                            <button class="flex justify-center items-center w-full text-gray-900 px-4 py-3 rounded-md focus:outline-none" v-on:click="toggleModal()">
                                <svg class="w-6 h-6 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg> Annuler
                            </button>
                            <button @click="sendDelete" v-on:click="toggleModal()" class="bg-red-500 flex justify-center items-center w-full text-white px-4 py-3 rounded-md focus:outline-none">Supprimer</button>
                        </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div v-if="showModal" class="opacity-25 fixed inset-0 z-40 bg-black"></div>
    </div>
</template>

<script>
export default {
name: "delete-ad-modal",
  data() {
    return {
      showModal: false,
      adToDelete: {}
    }
  },
  props:{
    buttonText: String,
    ad: Object
  },
  created() {
    this.adToDelete.title = this.ad.title,
    this.adToDelete._id = this.ad._id
  },
  methods: {
    toggleModal: function(){
      this.showModal = !this.showModal;
    },
    sendDelete(){
      this.$emit('deletingAd', this.adToDelete._id);
    }
  }
}
</script>

<style>

</style>