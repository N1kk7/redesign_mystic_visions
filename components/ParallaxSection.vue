<template>
  <section ref="section" class="parallax" id="author">
    <div ref="bg" class="parallax__bg">
      <div class="parallax_overlay"></div>
    </div>
    <div class="parallax_text">
      <strong class="strong_top" ref="text1">
        The framework outlined in The Pillars of Wisdom was not developed in
        theory.
      </strong>

      <p ref="text2">
        People find this book when they've become tired of platitudes,
        shortcuts, and advice that doesn't lead anywhere.
        It was shaped through decisions made in real-life situations influenced
        by real tradeoffs. And developed by working directly with people seeking
        long-term stability. People who had to navigate rising living costs and
        declining incentives.
               For three years now, GLO has helped people adopt this framework. Helping
        them reassess their environments and improve their living conditions.
        The framework has been pressure-tested by readers that are now living
        abroad. It has been refined through repeated application, and has
        endorsements from academic institutions. The ideas are not aspirational
        concepts. They are practical lenses that have been formed under
        pressure.
      </p>
      <strong class="strong_bottom" ref="text3">
        This book is not advice written from a distance. It is a result of
        choices with consequences that have already been made, and paths already
        taken.
      </strong>
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
const text3 = ref(null);

let ticking = false;

const handleScroll = () => {
  if (!section.value || !bg.value || ticking) return;

  ticking = true;

  requestAnimationFrame(() => {
    const rect = section.value.getBoundingClientRect();
    const vh = window.innerHeight;

    const progress = Math.min(
      1,
      Math.max(0, (vh - rect.top) / (vh + rect.height)),
    );

    const maxTranslate = bg.value.offsetHeight - section.value.offsetHeight;

    bg.value.style.transform = `translateY(${-maxTranslate * progress}px)`;

    ticking = false;
  });
};

onMounted(async () => {
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

  const texts = [text1.value, text2.value, text3.value];

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
  padding: 350px 0 70px;
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
      font-size: clamp(0.9rem, 2.3vw, 1.3rem);

      font-family: "Josefin Sans", sans-serif;
      font-weight: 400;
      line-height: 130%;
    max-width: 90%;
    gap: 20px;
    z-index: 1;
    will-change: transform;
    background: rgba(0, 0, 0, 0.7);
    border: 1px solid rgba(255, 255, 255, 0.3);
    backdrop-filter: blur(10px);
    text-align: center;
    border-radius: 40px;
    padding: 5%;

    .strong_top {
      // transform: translateY(-20px);
      padding-bottom: 20px;
      // white-space: nowrap;
      font-size: clamp(0.95rem, 2.5vw, 1.6rem);
      font-family: "Libre Baskerville", sans-serif;
      font-weight: 700;
      line-height: 130%;
      margin: 0 auto;
      @media screen and (max-width: 768px) {
        padding-bottom: 10px
      }

    }

    .strong_bottom {
      font-size: clamp(0.75rem, 2.1vw, 1.3rem);

      font-family: "Libre Baskerville", sans-serif;
      font-weight: 700;
      line-height: 130%;
    }

    // @media screen and (max-width: 1024px) {
    //   max-width: 90%;
    // }

    @media screen and (max-width: 768px) {
      line-height: 120%;
      // max-width: 90%;
      // font-size: 1.5rem;
    }

    @media screen and (max-width: 480px) {
      max-width: 95%;
      line-height: 110%;
      padding: 5% 4%;
      // font-size: 1.35rem;
    }
    @media screen and (max-width: 375px) {
      // font-size: 1.25rem;
    }
  }
}
</style>
