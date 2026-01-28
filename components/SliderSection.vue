<template>
  <section class="slider_section" ref="sectionRef" id="book">
    <div class="container">
      <div class="slider_section_content">
        <ClientOnly>
          <div class="swiper_wrapper" ref="sliderRef">
            <Swiper
              :modules="modules"
              navigation
              pagination
              mousewheel
              keyboard
              class="mySwiper"
            >

              <SwiperSlide v-for="img in sliderData" :key="img.id">
                <NuxtImg
                  :src="img.imgPath"
                  alt="slider"
                  width="450"
                  height="600"
                  priority
                />
              </SwiperSlide>
            </Swiper>
          </div>
        </ClientOnly>

        <div class="info_wrapper" ref="infoRef">
          <h3>The Pillars of Wisdom</h3>

          <div class="text_wrapper">
            <strong>
              The Pillars of Wisdom is not motivation or self-help.
            </strong>
            <p>
              It points out the patterns that matter: Investing your time and
              effort in the modern world; Why all effort isn't equal; Stepping
              outside the system instead of trying to win inside it.
            </p>
            <p>
              This book doesn't push you to escape your life. It helps you see
              it clearly by giving you a map.
            </p>
          </div>

          <NuxtLink class="slider_link" to="/">
            Explore the framework
          </NuxtLink>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { Swiper, SwiperSlide } from "swiper/vue";
import { Navigation, Pagination } from "swiper/modules";
import { ref, onMounted, nextTick } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";

const modules = [Navigation, Pagination];

const sliderData = ref([
  {
    id: 1,
    imgPath: "/images/slider1.jpg",
  },
  {
    id: 2,
    imgPath: "/images/slider2.jpg",
  },
  {
    id: 3,
    imgPath: "/images/slider3.jpg",
  },
  {
    id: 4,
    imgPath: "/images/slider4.jpg",
  },
]);

const sectionRef = ref(null);
const sliderRef = ref(null);
const infoRef = ref(null);

onMounted(async () => {
  await nextTick();

  const isMobile = window.innerWidth < 1024;
  gsap.from(sliderRef.value, {
    scrollTrigger: {
      trigger: sliderRef.value,
      start: "top 60%",
      toggleActions: "play none none none",
    },
    opacity: 0,
    x: isMobile ? 0 : -50,
    y: isMobile ? -50 : 0,
    duration: 0.8,
    ease: "power3.out",
  });

  const textEls = infoRef.value.querySelectorAll("h3, strong, p, .slider_link");
  gsap.from(textEls, {
    scrollTrigger: {
      trigger: infoRef.value,
      start: "top 65%",
      toggleActions: "play none none none",
    },
    opacity: 0,
    x: isMobile ? 0 : 50,
    y: isMobile ? 50 : 0,
    duration: 0.7,
    ease: "power3.out",
    stagger: 0.2,
  });
});
</script>

<style lang="scss">
.slider_section {
  width: 100%;
  height: auto;
  position: relative;
  overflow: hidden;
  padding-block: 128px;

  .mySwiper {
    --swiper-navigation-color: #fff;
    --swiper-pagination-bullet-inactive-color: rgba(255, 255, 255, 0.8);
    --swiper-pagination-color: #fff;
    box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
    border-radius: 22px;

    .swiper-button-next,
    .swiper-button-prev {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      background: rgba(0, 0, 0, 0.7);
      opacity: 0;
      pointer-events: none;
      transition:
        opacity 0.25s ease,
        transform 0.25s ease;

      svg {
        width: 15px;
        height: 15px;
      }
    }

    .swiper-pagination-bullet-active {
      width: 30px;
      border-radius: 5px;
    }

    @media screen and (min-width: 1024px) {
      &:hover {
        .swiper-button-next,
        .swiper-button-prev {
          opacity: 1;
          pointer-events: auto;
          transform: translateY(-50%) scale(0.95);
        }
      }
    }
  }

  &_content {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: space-between;
    align-items: stretch;
    gap: 64px;

    @media screen and (max-width: 1300px) {
      gap: 32px;
    }

    @media screen and (max-width: 1024px) {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      gap: 64px;
    }

    @media screen and (max-width: 768px) {
      gap: 48px;
    }
    @media screen and (max-width: 480px) {
      gap: 36px;
    }
    @media screen and (max-width: 375px) {
      gap: 32px;
    }
  }

  .swiper_wrapper {
    max-width: 50%;
    width: 450px;
    height: 600px;
    aspect-ratio: 3 / 4;
    flex: 0 0 40%;

    .swiper-slide {
      overflow: hidden;
      border-radius: 22px;

      img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
        // object-fit: contain;
      }
    }

    @media screen and (max-width: 1024px) {
      max-width: unset;
      height: auto;
    }

    @media screen and (max-width: 768px) {
      max-width: 90%;
    }

    @media screen and (max-width: 480px) {
      max-width: 100%;
    }
  }

  .info_wrapper {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-start;
    background: white;
    border-radius: 40px;
    padding: 6% 2vw;
    border: 1px solid black;

    h3 {
      font-size: clamp(1.875rem, 3vw, 2.5rem);
      font-weight: 700;
      font-family: "Libre Baskerville", sans-serif;
      white-space: nowrap;
      font-style: normal;
      line-height: 150%;

      @media screen and (max-width: 768px) {
        font-size: 1.875rem;
        line-height: 130%;
      }

      @media screen and (max-width: 480px) {
        font-size: clamp(1.2rem, 7vw, 1.6rem);
        padding-top: 10px;
      }

      // @media screen and (max-width: 375px) {
      //   font-size: 1.5rem;

      // }
    }

    strong,
    p {
      font-size: 1.25rem;
      font-weight: 400;
      font-family: 'Josefin Sans', sans-serif;

      font-style: normal;
      line-height: 150%;

      @media screen and (max-width: 768px) {
        font-size: 1.125rem;
        line-height: 130%;
      }
    }
    p {
      font-weight: 400;
    }

    strong {
      font-family: "Libre Baskerville", sans-serif;
      font-weight: 700;
    }

    .slider_link {
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: "Libre Baskerville", sans-serif;
      font-weight: 700;
      // background: rgb(253, 130, 43);
      background: #f7ac0b;
      border-radius: 20px;
      color: white;
      font-size: 1rem;
      padding: 16px 32px;

      @media screen and (min-width: 1024px) {
        &:hover {
          // background: rgb(255, 112, 10);
          background: #f0a607;

          transition: all ease 0.3s;
        }
      }

      &:active {
        // background: rgb(255, 112, 10);
        background: #f0a607;

        transition: all ease 0.3s;
      }
    }

    @media screen and (max-width: 1024px) {
      gap: 40px;
    }

    @media screen and (max-width: 768px) {
      padding: 6%;
      width: 100%;
      gap: 35px;
    }
    @media screen and (max-width: 425px) {
      gap: 25px;
    }
    @media screen and (max-width: 375px) {
      gap: 20px;
    }
  }

  .text_wrapper {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-start;
    gap: 32px;

    @media screen and (max-width: 768px) {
      gap: 25px;
    }
    @media screen and (max-width: 425px) {
      gap: 20px;
    }
    @media screen and (max-width: 375px) {
      gap: 15px;
    }
  }

  @media screen and (max-width: 1024px) {
    padding-block: 100px;
  }

  @media screen and (max-width: 768px) {
    padding-block: 80px;
  }

  @media screen and (max-width: 425px) {
    padding-block: 70px;
  }

  @media screen and (max-width: 375px) {
    padding-block: 60px;
  }
}
</style>
