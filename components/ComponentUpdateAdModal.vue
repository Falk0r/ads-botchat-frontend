<template>
  <div>
    <button class="bg-blue-500 text-white active:bg-pink-600 font-bold uppercase text-sm px-6 py-3 rounded shadow hover:shadow-lg outline-none focus:outline-none mr-1 mb-1" type="button" style="transition: all .15s ease" v-on:click="toggleModal()">
      {{buttonText}}
    </button>
    <div v-if="showModal" class="overflow-x-hidden overflow-y-auto fixed inset-0 z-50 outline-none focus:outline-none justify-center items-center flex">
      <div class="relative py-3 sm:max-w-xl sm:mx-auto">
        <div class="relative px-4 py-10 bg-white mx-8 md:mx-0 shadow rounded-3xl sm:p-10">
          <div class="max-w-md mx-auto">
            <div class="flex items-center space-x-5">
              <div class="h-14 w-14 bg-yellow-200 rounded-full flex flex-shrink-0 justify-center items-center text-yellow-500 text-2xl font-mono">E</div>
              <div class="block pl-2 font-semibold text-xl self-start text-gray-700">
                <h2 class="leading-relaxed">Editer une Pub</h2>
                <p class="text-sm text-gray-500 font-normal leading-relaxed">Edite les champs ci-dessous pour mettre à jour ta pub.</p>
              </div>
            </div>
            <div class="divide-y divide-gray-200">
              <div class="py-8 text-base leading-6 space-y-4 text-gray-700 sm:text-lg sm:leading-7">
                <div class="flex flex-col">
                  <label class="leading-loose">Texte</label>
                  <input v-model="adToUpdate.text" type="text" class="px-4 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600">
                </div>
                <div class="flex flex-col">
                  <label class="leading-loose">Image</label>
                  <input v-model="adToUpdate.image" type="text" class="px-4 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600">
                  <div class="flex flex-wrap justify-center">
                    <div class="w-6/12 sm:w-4/12 px-4">
                      <img :src="adToUpdate.image" alt="..." class="shadow rounded max-w-full h-auto align-middle border-none" />
                    </div>
                  </div>
                </div>
                <div class="flex flex-col">
                  <label class="leading-loose">Lien de la pub</label>
                  <input v-model="adToUpdate.url" type="text" class="px-4 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600">
                </div>
              </div>
              <div class="pt-4 flex items-center space-x-4">
                  <button class="flex justify-center items-center w-full text-gray-900 px-4 py-3 rounded-md focus:outline-none" v-on:click="toggleModal()">
                    <svg class="w-6 h-6 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg> Annuler
                  </button>
                  <button @click="sendUpdate" v-on:click="toggleModal()" class="bg-blue-500 flex justify-center items-center w-full text-white px-4 py-3 rounded-md focus:outline-none">Modifier</button>
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
  name: "update-ad-modal",
  data() {
    return {
      showModal: false,
      adToUpdate: {}
    }
  },
  props:{
    buttonText: String,
    ad: Object
  },
  created() {
    this.adToUpdate.text = this.ad.text,
    this.adToUpdate.image = this.ad.image,
    this.adToUpdate.url = this.ad.url,
    this.adToUpdate._id = this.ad._id
  },
  methods: {
    toggleModal: function(){
      this.showModal = !this.showModal;
    },
    sendUpdate(){
      this.$emit('updatingAd', this.adToUpdate);
    }
  }
}
</script>