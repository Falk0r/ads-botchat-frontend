<template>
  <!-- component -->
    <!-- item card -->
    <div class="md:flex shadow-lg my-2 max-w-lg md:max-w-2xl h-64 mx-6 md:mx-auto rounded">
        <img class="h-full w-full md:w-1/3  object-cover rounded-l-lg rounded-r-none pb-5/6" :src="ad.image" alt="bag">
        <div class="w-full md:w-2/3 px-4 py-4 bg-white rounded-r-lg flex flex-col justify-between">
            <div class="flex items-center">
                <h2 class="text-xl text-gray-800 font-medium mr-auto">{{ ad.title}}</h2>
                <p class="font-semibold tracking-tighter bg-green-300 px-4 py-1 text-green-800 rounded" v-if="ad.status == 'publish'">
                    Online
                </p>
                <p class="font-semibold tracking-tighter bg-red-300 px-4 py-1 text-red-800 rounded" v-else>
                    Offline
                </p>
            </div>
            <p class="text-sm text-gray-700 mt-4 h-3/7 overflow-hidden">
                {{ad.text}}
            </p>
            <div class="flex items-center justify-end mt-4 top-auto">
                <!-- <button class="bg-white text-red-500 px-4 py-2 rounded mr-auto hover:underline">Delete</button> -->
                <component-delete-ad-modal buttonText="Supprimer" :ad="ad" v-on="$listeners" />
                <component-update-ad-modal buttonText="Editer" :ad="ad" v-on="$listeners"/>
                <component-publish-ad-modal v-if="ad.status == 'publish'" buttonText="Dépublier" :ad="ad" v-on="$listeners"/>
                <component-publish-ad-modal v-else buttonText="Publier" :ad="ad" v-on="$listeners"/>
            </div>
        </div>
    </div>
</template>

<script>
import ComponentDeleteAdModal from './ComponentDeleteAdModal.vue'
import ComponentPublishAdModal from './ComponentPublishAdModal.vue'
import ComponentUpdateAdModal from './ComponentUpdateAdModal.vue'
export default {
  components: { ComponentUpdateAdModal, ComponentDeleteAdModal, ComponentPublishAdModal },
    props:{
    ad: Object
  },
}
</script>

<style>

</style>