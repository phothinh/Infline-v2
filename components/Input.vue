<template>
  <div class="flex flex-col items-start w-[30vw]">
    <h3 class="text-[0.8vw] font-poppins text-[#999999] mb-1">{{ label }}</h3>

    <div class="flex items-center w-full border-b-2 border-[#000842] pb-2">
      <img src="@/assets/img/icons/mail.svg" alt="img" class="h-3 mr-3">
      <input type="email" class="bg-transparent placeholder-[#000842] font-poppins text-[0.8vw] w-full focus:outline-none" :placeholder="placeholder">
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
    imgUrl: {
      type: String,
      required: false,
    },
    placeholder: {
      type: String,
      required: true,
    },
  }
};
</script>
