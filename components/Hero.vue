<template>
  <section class="hero">
    <div class="container">
      <div class="hero_content">
        <!-- <NuxtImg
          class="hero_bg"
          src="/images/hero_bg.webp"
          alt="hero_bg"
          width="800"
          height="500"
          priority
        >
        </NuxtImg> -->
        <div class="hero_overlay"></div>
        <video
        ref="videoRef"
            class="hero_video"
            playsinline
            autoplay
            muted
            loop
            preload="auto"
            poster="../public/images/video_preview.webp"
        >
            <!-- <source 
                src="../public/videos/hero-final-cropped1.mp4" 
                type="video/mp4" 
            /> -->
                <source 
                src="../public/videos/video_web.mp4" 
                type="video/mp4" 
            />
            Your browser does not support the video tag.
        </video>

        <div class="text_content" ref="contentRef">
          <h1 class="h1_title" style="opacity: 0;">
            You saw beyond what you <br />
            were taught in school.
          </h1>
          <div class="text_wrapper">
            <p class="text_start" style="opacity: 0;">
              That's how you paid attention to who the rules actually helped.
            </p>
            <p class="text_second" style="opacity: 0;">
              That's why you didn't fail the system, you noticed how it works.
            </p>
          </div>

          <NuxtLink
          style="opacity: 0;"
            class="hero_link"
            to="https://shop.thepillarsofwisdom.com/checkouts/cn/hWN7trf773GcZCs4hUkcyRzF/en-mx?_r=AQABaYj4HQ9OB9KSkMAVLS0Q8JkjjGz4J5dDJ66MP71HAOk&auto_redirect=false&edge_redirect=true&skip_shop_pay=true"
            target="_blank"
          >
            Read The Pillars of Wisdom
          </NuxtLink>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, nextTick } from "vue";
import { gsap } from "gsap";


// const imgRef = ref(null);
const contentRef = ref(null);
const videoRef = ref(null);

function startAnimation() {
  if (!contentRef.value) return;

  const contentEls = contentRef.value.querySelectorAll(
    ".h1_title, .text_start, .text_second, .hero_link"
  );

  if (!contentEls.length) return;
  

  gsap.fromTo(
    contentEls,
    { opacity: 0, y: 30 },
    {
      opacity: 1,
      y: 0,
      delay: 0,
      stagger: 0.20,
      duration: 0.7,
      ease: "power3.out",
      clearProps: "all",
    }
  );
}

onMounted(async () => {
  await nextTick();
  startAnimation();
});

</script>




<style lang="scss">
.hero {
  width: 100vw;
  height: 100vh;
  position: relative;
  display: block;

  &_overlay {
    position: absolute;
    background: rgba(0,0,0,0.35);
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    z-index: 1;
  }

  &_content {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
  }


  &_video {
    width: 100%;
    height: 100%;
    padding-top: var(--header-height);
    transition: all ease 0.3s;
    position: absolute;
    object-fit: cover;
    top: 0;
    left: 0;
  }

  .text_content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: white;
    position: relative;
    padding-top: 10%;
    z-index: 1;
    width: 100%;
    height: 100%;
    gap: 40px;

    @media screen and (max-width: 480px) {
      gap: 25px;
    }
    @media screen and (max-width: 375px) {
      gap: 15px;
    }
  }

  h1 {
    font-family: "Libre Baskerville", sans-serif;
    font-size: clamp(1.5rem, 5vw, 4.5rem);
    font-weight: 700;
    text-align: center;
    line-height: 1.2;
  }

  .text_wrapper {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-start;
    font-family: 'Josefin Sans', sans-serif;
    font-weight: 400;
    font-size: 1.5rem;
    gap: 24px;

    @media screen and (max-width: 768px) {
        text-align: center;

        font-size: clamp(1.125rem, 2vw, 1.5rem);
    }
  }

  .hero_link {
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: "Libre Baskerville", sans-serif;

      // background: rgb(253, 130, 43);
      background: #F7AC0B;

      font-weight: 700;
      margin-top: 20px;
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

      @media screen and (max-width: 480px) {
        padding: 12px 20px;
        font-size: 0.8rem;
      }
      @media screen and (max-width: 375px) {
        padding: 8px 10px;
        font-size: 0.7rem;


      }


      &:active {
        // background: rgb(255, 112, 10);
          background: #f0a607;

        transition: all ease 0.3s;
      }


  }
}
</style>
