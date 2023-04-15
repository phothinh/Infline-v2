<template>
  <div class="flex flex-col items-start w-[30vw]">
    <h3 class="text-[0.8vw] font-poppins text-[#999999] mb-1">{{ label }}</h3>
    <div class="flex items-center w-full border-b-2 border-[#999999] pb-2">
      <img src="@/assets/img/icons/mdp.svg" class="h-4 mr-3">
      <input :type="showPassword ? 'text' : 'password'" class="bg-transparent placeholder-[#000842] font-poppins text-[0.8vw] w-full focus:outline-none" :placeholder="placeholder" v-model="password">
      <img v-if="showEyeIcon" src="@/assets/img/icons/eye.svg" class="h-4 ml-auto" @click="showPassword = !showPassword">
    </div>

    <div v-if="!hideCheckbox" class="flex items-center justify-between w-full mt-4">
      <div class="flex items-center">
          <input type="checkbox" class="mr-1">
          <span class="text-[0.8vw] font-poppins text-black">Se souvenir de moi</span>
      </div>
      <a v-if="showForgotPasswordLink" :href="forgotPasswordLink" class="text-[0.8vw] font-poppins text-[#4D4D4D] hover:text-infline-purple">{{ forgotPasswordText }}</a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      required: true,
    },
    placeholder: {
      type: String,
      required: true,
    },
    forgotPasswordLink: {
      type: String,
      required: false,
    },
    forgotPasswordText: {
      type: String,
      required: false,
    },
    showCheckbox: {
      type: Boolean,
      default: true,
    },
    showForgotPasswordLink: {
      type: Boolean,
      default: true,
    },
    showEyeIcon: {
      type: Boolean,
      default: true,
    },
    hideCheckbox: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      password: '',
      showPassword: false,
    };
  },
};
</script>
