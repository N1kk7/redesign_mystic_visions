<template>
  <section ref="section" class="parallax">
    <div ref="bg" class="parallax__bg">
    <div class="parallax_overlay"></div>

    </div>
    <div class="parallax_text">
      <p ref="text1">
        People who read this aren't looking for permission. They prefer a clear
        vision over optimism.
      </p>

      <p ref="text2">
        People find this book when they've become tired of platitudes,
        shortcuts, and advice that doesn't lead anywhere.
      </p>
    </div>
  </section>
</template>


<script setup>
import { ref, onMounted, onUnmounted, nextTick } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const section = ref(null);
const bg = ref(null);
const text1 = ref(null);
const text2 = ref(null);

let ticking = false;

const handleScroll = () => {
  if (!section.value || !bg.value || ticking) return;

  ticking = true;

  requestAnimationFrame(() => {
    const rect = section.value.getBoundingClientRect();
    const vh = window.innerHeight;

    const progress = Math.min(
      1,
      Math.max(0, (vh - rect.top) / (vh + rect.height))
    );

    const maxTranslate = bg.value.offsetHeight - section.value.offsetHeight;

    bg.value.style.transform = `translateY(${-maxTranslate * progress}px)`;

    ticking = false;
  });
};

onMounted(async() => {


  handleScroll();
  window.addEventListener("scroll", handleScroll, { passive: true });

  await nextTick();

  // const text = [text1.value, text2.value];

  // gsap.to(text, {
  //   y: -100, 
  //   ease: "none",
  //   scrollTrigger: {
  //     trigger: section.value,
  //     start: "top bottom",
  //     end: "bottom top",  
  //     scrub: true,
  //   },
  // });

  const texts = [text1.value, text2.value];

  gsap.set(texts, {
    opacity: 0,
    y: 40,
  });

  gsap.to(texts, {
    opacity: 1,
    y: 0,
    duration: 0.8,
    ease: "power3.out",
    stagger: 0.4, 
    scrollTrigger: {
      trigger: section.value,
      start: "top 40%",
      toggleActions: "play none none none",
    },
  });
});


onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<style lang="scss">


    .parallax {
        width: 100%;
        height: auto;
        position: relative;
        // background: #898989;
        color: white;
        padding-block: 192px;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;

        &_overlay {
          width: 100%;
          height: 100%;
          position: absolute;
          background: rgba(0, 0, 0, 0.45);
          top: 0;
          left: 0;
          z-index: 1;
        }

        &__bg {

            position: absolute;
            left: 0;
            top: 10%;
            width: 100%;
            height: 140%;
            transform: translateY(-50%);
            background-image: url("@/public/images/parallax_bg.webp");
            background-size: cover;
            background-position: center;
            will-change: transform;
            background-repeat: no-repeat;

        }

        &_text {
            display: flex;
            flex-direction: column;
            justify-content: flex-start;
            align-items: flex-start;
            max-width: 70%;
            gap: 40px;
            z-index: 1;
            font-family: 'Roboto', sans-serif;
            font-weight: 700;
            font-size: 1.8rem;
            line-height: 150%;
            text-align: baseline;
            will-change: transform;

            @media screen and (max-width: 1024px) {
              max-width: 80%;
            }

            @media screen and (max-width: 768px) {
              max-width: 90%;
              font-size: 1.5rem;
            }

            @media screen and (max-width: 480px) {
              max-width: 95%;
              font-size: 1.35rem;
            }
            @media screen and (max-width: 375px) {
              font-size: 1.25rem;
            }
            
        }
    }
</style>
