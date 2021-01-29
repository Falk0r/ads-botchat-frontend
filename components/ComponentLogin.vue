<template>
  <!-- component -->
<!-- This is an example component -->
<div class="h-screen font-sans login bg-cover">
<div class="container mx-auto h-full flex flex-1 justify-center items-center">
    <div class="w-full max-w-lg">
      <div class="leading-loose">
        <div class="max-w-sm m-4 p-10 bg-white bg-opacity-25 rounded shadow-xl">
            <p class="text-white font-medium text-center text-lg font-bold">LOGIN</p>
            <div class="">
                <label class="block text-sm text-white" for="email">E-mail</label>
                <input class="w-full px-5 py-1 text-gray-700 bg-gray-300 rounded focus:outline-none focus:bg-white" 
                    v-model="user.email" type="email" id="email"  placeholder="e-mail" aria-label="email" required>
            </div>
            <div class="mt-2">
                <label class="block  text-sm text-white">Mot de passe</label>
                <input class="w-full px-5 py-1 text-gray-700 bg-gray-300 rounded focus:outline-none focus:bg-white"
                    v-model="user.password" type="password" id="password" placeholder="mot de passe" arial-label="password" required>
            </div>
            <div class="mt-4 items-center flex justify-between">
                <button class="px-4 py-1 text-white font-light tracking-wider bg-gray-900 hover:bg-gray-800 rounded"
                    @click="sendLogin">Se connecter</button>
                <a class="inline-block right-0 align-baseline font-bold text-sm text-500 text-white hover:text-red-400"
                    href="#">Mot de passe perdu ?</a>
            </div>
            <div class="text-center">
                <h3 class="inline-block right-0 align-baseline font-light text-sm text-500 hover:text-red-400">
                    {{message}}
                </h3>
              </div>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
    data() {
      return {
          user : {
              email: null,
              password: null
          }
      }
    },
    props:{
        message: String
    },
    methods: {
        sendLogin(){
            this.$emit('logingUser', this.user);
        }
    }
}
</script>

<style>
    .login{
    /*
    background: url('https://tailwindadmin.netlify.app/dist/images/login-new.jpeg');
    */
    background: url('http://bit.ly/2gPLxZ4');
    background-repeat: no-repeat;
    background-size: cover;
}
</style>