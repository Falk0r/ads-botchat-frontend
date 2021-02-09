<template>
    <div>
        <button class="bg-blue-600 text-gray-200 px-2 py-2 rounded-md" type="button" style="transition: all .15s ease" v-on:click="toggleModal()">
        {{buttonText}}
        </button>
        <div v-if="showModal" class="overflow-x-hidden overflow-y-auto fixed inset-0 z-50 outline-none focus:outline-none justify-center items-center flex">
            <div class="relative py-3 sm:max-w-xl sm:mx-auto">
                <div class="relative px-4 py-10 bg-white mx-8 md:mx-0 shadow rounded-3xl sm:p-10">
                    <div class="max-w-md mx-auto">
                        <div class="flex items-center space-x-5">
                            <div v-if="adToPublish.status == 'publish'" class="h-14 w-14 bg-blue-200 rounded-full flex flex-shrink-0 justify-center items-center text-blue-500 text-2xl font-mono">D</div>
                            <div v-else class="h-14 w-14 bg-blue-200 rounded-full flex flex-shrink-0 justify-center items-center text-blue-500 text-2xl font-mono">P</div>
                            <div v-if="adToPublish.status == 'publish'" class="block pl-2 font-semibold text-xl self-start text-gray-700">
                                <h2 class="leading-relaxed">Dépublier la Pub</h2>
                                <p class="text-sm text-gray-500 font-normal leading-relaxed">On enlève la pub des réseaux ?</p>
                            </div>
                            <div v-else class="block pl-2 font-semibold text-xl self-start text-gray-700">
                                <h2 class="leading-relaxed">Publier la Pub</h2>
                                <p class="text-sm text-gray-500 font-normal leading-relaxed">On envoie la pub sur les réseaux ?</p>
                            </div>
                        </div>
                        <div class="divide-y divide-gray-200">
                        <div class="py-8 text-base leading-6 space-y-4 text-gray-700 sm:text-lg sm:leading-7">
                            <div class="flex flex-col">
                            <label class="leading-loose">Titre</label>
                            <p class="px-4 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600">{{adToPublish.title}}</p>
                            </div>
                        </div>
                        <div class="py-8 text-base leading-6 space-y-4 text-gray-700 sm:text-lg sm:leading-7">
                            <div class="flex flex-col">
                            <label class="leading-loose">Lien</label>
                            <p class="px-4 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600">{{adToPublish.script}}</p>
                            </div>
                        </div>
                        <div class="pt-4 flex items-center space-x-4">
                            <button class="flex justify-center items-center w-full text-gray-900 px-4 py-3 rounded-md focus:outline-none" v-on:click="toggleModal()">
                                <svg class="w-6 h-6 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg> Annuler
                            </button>
                            <button @click="sendPublish" v-on:click="toggleModal()" v-if="adToPublish.status == 'publish'" class="bg-blue-500 flex justify-center items-center w-full text-white px-4 py-3 rounded-md focus:outline-none">Dépublier</button>
                            <button @click="sendPublish" v-on:click="toggleModal()" v-else class="bg-blue-500 flex justify-center items-center w-full text-white px-4 py-3 rounded-md focus:outline-none">Publier</button>
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
name: "publish-ad-modal",
  data() {
    return {
      showModal: false,
      adToPublish: {}
    }
  },
  props:{
    buttonText: String,
    ad: Object
  },
  created() {
    this.adToPublish = this.ad;
    this.adToPublish.script = '\<script src=\"http://127.0.0.1:5000/js-customers/'+ this.adToPublish._id +'\"\>\<\/script\>';
  },
  methods: {
    toggleModal: function(){
      this.showModal = !this.showModal;
    },
    sendPublish(){
      if (this.adToPublish.status === "publish") {
          this.adToPublish.status = "pending";
      } else {
          this.adToPublish.status = "publish";
      }
      this.$emit('publishingAd', this.adToPublish);
    }
  }
}
</script>

<style>

</style>