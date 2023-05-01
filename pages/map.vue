<template>
    <div class="flex h-screen">
        <div class="flex flex-col mt-[2vw] ml-[4vw]">
            <h1 class="text-left text-[1.5vw] font-integral uppercase"><span @click="redirectToHome" class="hover:cursor-pointer">Infline</span></h1>
            <h1 class="text-left text-[2vw] font-integral uppercase mt-[1.7vw]">Hello,</h1>
            <p class="text-left text-[0.8vw font-poppins]">Trouve l'influenceur qu'il te faut ici !</p>
            
            <div class="flex flex-col items-center justify-center w-[56vw] h-[26vw] mt-[1vw]">
                <Mapbox
                :access-token="accessToken"
                :center="{ lat: 45.899247, lng: 6.129384 }"
                :zoom="12"
                :markers="markers"
                />
            </div>

            <Button class="mt-[1vw] uppercase" bgColor="bg-infline-purple" textColor="text-white" buttonText="Rechercher Ici" />
        </div>

    </div>
  </template>

<script>
import Mapbox from '~/components/Map/Mapbox.vue';

export default {
  components: {
    Mapbox
  },
  methods:{
    redirectToHome() {
            this.$router.push('/');
    },
  },
  data() {
    return {
      accessToken: 'pk.eyJ1IjoiaGVucmktcHRoIiwiYSI6ImNsZTc3Z2FoNDAyczAzdXBoY3ppbDNxeW8ifQ.uBIZ4Wsw72kLND_S81Eurg',
      markers: [
        {
          coordinates: [6.129384, 45.899247],
          // imageUrl: '@/assets/img/photos/selfie.svg',
          title: "Marie, influenceuse beauté",
          description: "Hello, moi c’est Marie, 24 ans. Je suis influenceuse beauté depuis plus de 3 ans, spécialiste Insta et TikTok",
        },
        {
          coordinates: [6.122384, 45.887247],
          // imageUrl: '@/assets/img/photos/selfie.svg',
          title: "Jo, influenceuse beauté",
          description: "Hello, moi c’est Marie, 24 ans. Je suis influenceuse beauté depuis plus de 3 ans, spécialiste Insta et TikTok",
        }, 
        {
          coordinates: [6.102384, 45.880247],
          // imageUrl: '@/assets/img/photos/selfie.svg',
          title: "Ja, influenceuse beauté",
          description: "Hello, moi c’est Marie, 24 ans. Je suis influenceuse beauté depuis plus de 3 ans, spécialiste Insta et TikTok",
        }, 
        {
          coordinates: [6.100384, 45.910247],
          // imageUrl: '@/assets/img/photos/selfie.svg',
          title: "Ju, influenceuse beauté",
          description: "Hello, moi c’est Marie, 24 ans. Je suis influenceuse beauté depuis plus de 3 ans, spécialiste Insta et TikTok",
        },  
      ]
    };
  }
};
</script>
