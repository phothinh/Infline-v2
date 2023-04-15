<template>
    <div class="flex h-screen">
        <!-- Partie gauche -->
        <div class="flex-1">
            <div class="flex flex-col">
                <h2 class="text-left text-[1.5vw] mt-[2vw] ml-[4vw] font-integral uppercase"><span @click="redirectToHome" class="hover:cursor-pointer">Infline</span></h2>
                <div class="flex flex-col items-center justify-center">
                    <div class="flex flex-col">
                        <h2 class="text-left text-[1.5vw] font-integral uppercase mt-[3vw]">Se connecter</h2>
                        <p class="text-left text-[0.8vw] font-poppins mt-[1.5vw]">Si tu n’es pas encore inscrit,<br>Tu peux  <span @click="redirectToRegister" class="font-bold text-infline-purple hover:cursor-pointer">t’inscrire ici !</span></p>
                        <!-- <Input v-model="email" type="email" label="Email" imgURL="@/assets/img/icons/mail.svg" placeholder="Entre ton adresse e-mail" class="mt-[2vw]"/>
                        <InputMDP v-model="password" type="password" label="Mot de passe" showEyeIcon="true" showForgotPasswordLink="true" forgotPasswordText="Mot de passe oublié ?" placeholder="Entre ton adresse mot de passe" class="mt-[2vw]"/>
                        <router-link :to="{ name: 'map' }">
                            <Button type="submit" class="mt-[3vw]" bgColor="bg-infline-purple" textColor="text-white" buttonText="Se connecter" />
                        </router-link> -->
                        <form @submit.prevent="userLogin"> 
                            <div v-if="err" class="mt-[1vw] p-4 mb-4 text-[0.8vw] text-red-700 bg-red-100 rounded-lg dark:bg-red-200 dark:text-red-800 " role="alert" >
                                 {{ err }} 
                            </div>

                            <div class="w-[30vw] border-b-2 border-[#000842] pb-2 mt-[1vw]"> 
                                <label for="email" class="text-[0.8vw] font-poppins text-[#999999] mb-1">Email</label > 
                                <input v-model="email" type="email" class="bg-transparent placeholder-[#000842] font-poppins text-[0.8vw] w-full focus:outline-none" placeholder="name@strapi.io" required /> 
                            </div>

                            <div class="w-[30vw] border-b-2 border-[#999999] pb-2 mt-[1vw]"> 
                                <label for="password" class="text-[0.8vw] font-poppins text-[#999999] mb-1" >Mot de passe</label > 
                                <input v-model="password" type="password" class="bg-transparent placeholder-[#000842] font-poppins text-[0.8vw] w-full focus:outline-none" placeholder="Entre ton mot de passe" required />  
                            </div> 
                            <p class="mt-2 text-sm text-gray-500 dark:text-gray-400"> 
                                <NuxtLink class="text-[0.8vw] font-poppins text-[#4D4D4D] hover:text-infline-purple" to="/user/forgot" >
                                    Mot de passe oublié ?
                                </NuxtLink > 
                            </p> 

                            <button type="submit" class="py-[1vw] px-[3vw] rounded-lg uppercase text-[0.8vw] font-integral bg-infline-purple text-white mt-[3vw]">
                                 Se connecter 
                            </button> 
                        </form>  
                        
                    </div>
                    <p class="font-poppins text-[0.8vw] text-[#B5B5B5] mt-[4vw]">ou continue avec</p>
                    <div class="flex justify-center items-center w-[2.2vw] space-x-3 mt-[1vw]">
                        <img src="@/assets/img/connexion/facebook.svg" alt="fb"/>
                        <img src="@/assets/img/connexion/apple.svg" alt="apple"/>
                        <img src="@/assets/img/connexion/google.svg" alt="google"/>
                    </div>
                </div>
            </div>
        
        </div>

        <!-- Partie droite -->
        <div class="flex-1">
            <LoginRegisterJoin class="w-full"/>
        </div>
    </div>
  </template>

<script>
export default {
    auth: 'guest',
      data() {
        return {
          err: null,
          email: '',
          password: '',
        }
      },
    methods: {
        redirectToRegister() {
            this.$router.push('/register');
        },
        redirectToHome() {
            this.$router.push('/');
        },
        async userLogin() {
            try {
                await this.$auth.loginWith('local', {
                    data: { identifier: this.email, password: this.password },
                })
            } catch (e) {
                if (e.response) this.err = e.response.data.error.message
            }
        },
    }
}
</script>