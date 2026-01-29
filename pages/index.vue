<template>
    <div class="page">

      <Hero/>
      <AboutBook/>
      <SliderSection />
      <ParallaxSection />
      <Reviews />
      <Secondary />

        <!-- <PromoHero/> -->
        <!-- <Book/> -->
        <!-- <Apparel/> -->
        <!-- <Consulting/> -->
        <!-- <Testimonnials/> -->
        <!-- <Quote/> -->
        <!-- <Consultations/> -->
        <!-- <Substack/> -->

        

        <!-- <TestComponent/> -->


    </div>
</template>


<script setup>
import { onMounted } from "vue";



if (import.meta.client) {
useHead({
  script: [
    {
      innerHTML: `
        !function(f,b,e,v,n,t,s)
        {if(f.fbq)return;n=f.fbq=function(){n.callMethod?
        n.callMethod.apply(n,arguments):n.queue.push(arguments)};
        if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';
        n.queue=[];t=b.createElement(e);t.async=!0;
        t.src=v;s=b.getElementsByTagName(e)[0];
        s.parentNode.insertBefore(t,s)}(window, document,'script',
        'https://connect.facebook.net/en_US/fbevents.js');
        fbq('init', '1541485453520508');
        fbq('track', 'PageView');
      `,
      type: 'text/javascript',
    },
  ],
  noscript: [
    {
      children: `
        <img height="1" width="1" style="display:none"
             src="https://www.facebook.com/tr?id=1541485453520508&ev=PageView&noscript=1" />
      `
    }
  ]
})


}


</script>



<style lang="scss">

  // .container {
  //   width: clamp(800px, 80vw, 1300px) !important;

  //   @media screen and (max-width: 1024px) {
  //     width: clamp(280px, 90vw, 1200px) !important;
  //   }
  //   @media screen and (max-width: 450px) {
  //     width: clamp(280px, 95vw, 1200px) !important;
  //   }
  // }


</style>