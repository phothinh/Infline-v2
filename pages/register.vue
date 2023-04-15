<template>
    <div class="flex h-screen">
        <!-- Partie gauche -->
        <div class="flex-1">
            <div class="flex flex-col">
              <h2 class="text-left text-[1.5vw] mt-[2vw] ml-[4vw] font-integral uppercase"><span @click="redirectToHome" class="hover:cursor-pointer">Infline</span></h2>
                <div class="flex flex-col items-center justify-center">
                    <div class="flex flex-col">
                      <h2 class="text-left text-[1.5vw] font-integral uppercase mt-[3vw]">S'inscrire</h2>
                      <p class="text-left text-[0.8vw] font-poppins mt-[1.5vw]">Tu es déjà inscrit ?<br>Tu peux  <span @click="redirectToLogin" class="font-bold text-infline-purple hover:cursor-pointer">te connecter ici</span></p>
                      <!--<Input v-model="email" type="email" label="Email" imgURL="@/assets/img/icons/mail.svg" placeholder="Entre ton adresse e-mail" class="mt-[2vw]"/>
                      <InputMDP v-model="password" type="password" label="Mot de passe" hideCheckbox placeholder="Entre ton adresse mot de passe" class="mt-[2vw]"/>
                      <InputMDP label="Confirmation de mot de passe" hideCheckbox placeholder="Confirme ton mot de passe" class="mt-[2vw]"/>
                      <Button type="submit" class="mt-[3vw]" bgColor="bg-infline-purple" textColor="text-white" buttonText="S'inscrire" />-->
                      <form @submit.prevent="userRegister">

                        <div v-if="err" class=" mt-[1vw] p-4 mb-4 text-[0.8vw] text-red-700 bg-red-100 rounded-lg dark:bg-red-200 dark:text-red-800" role="alert">
                          {{ err }}
                        </div>

                        <div v-if="success" class="mt-[1vw] p-4 mb-4 text-[0.8vw] text-green-700 bg-green-100 rounded-lg dark:bg-green-200 dark:text-green-800" role="alert">
                          Your account has been created successfully you can now
                          <NuxtLink class="font-medium" to="/login">Login</NuxtLink>
                        </div>

                        <div class="w-[30vw] border-b-2 border-[#000842] pb-2 mt-[1vw]">
                          <label for="username" class="text-[0.8vw] font-poppins text-[#999999] mb-1">Pseudo</label>
                          <input v-model="username" type="text" class="bg-transparent placeholder-[#000842] font-poppins text-[0.8vw] w-full focus:outline-none" placeholder="Entre ton pseudo" required />
                        </div>

                        <div class="w-[30vw] border-b-2 border-[#999999] pb-2 mt-[1vw]">
                          <label for="email" class="text-[0.8vw] font-poppins text-[#999999] mb-1" >Email</label >
                          <input v-model="email" type="email" class="bg-transparent placeholder-[#000842] font-poppins text-[0.8vw] w-full focus:outline-none" placeholder="Entre ton addresse mail" required />
                        </div>

                        <div class="w-[30vw] border-b-2 border-[#999999] pb-2 mt-[1vw]">
                          <label for="password" class="text-[0.8vw] font-poppins text-[#999999] mb-1" >Mot de passe</label >
                            <input v-model="password" type="password" class="bg-transparent placeholder-[#000842] font-poppins text-[0.8vw] w-full focus:outline-none" placeholder="Entre ton mot de passe" required />
                        </div>

                        <button type="submit" class="py-[1vw] px-[3vw] rounded-lg uppercase text-[0.8vw] font-integral bg-infline-purple text-white mt-[3vw]">
                          S'inscrire
                        </button>
                        
                      </form>
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
          success: false,
          err: null,
          username: '',
          email: '',
          password: '',
        }
      },
  methods: {
    async userRegister() {
          try {
            this.$axios.setToken(false)
            await this.$axios.post('auth/local/register', {
              username: this.username,
              email: this.email,
              password: this.password,
            })
            this.success = true
          } catch (e) {
            if (e.response) this.err = e.response.data.error.message
          }
        },
    redirectToLogin() {
      this.$router.push('/login');
    },
    redirectToHome() {
            this.$router.push('/');
        },
  }
}
</script>