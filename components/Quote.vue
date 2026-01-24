<template>
  <section class="section quote" ref="sectionRef" id="quote">
    <div class="quote_content">
      <div class="quote_text" ref="descriptionRef">
        <div class="line">
          <div class="left_items item">
            <span class="start">Lift</span>
          </div>
          <div class="right_items item">
            <span class="accent">Harder</span>
          </div>
        </div>
        <div class="line">
          <div class="left_items item">
            <span class="start">Read</span>
          </div>
          <div class="right_items item">
            <span class="accent">Smarter</span>
          </div>
        </div>
        <div class="line">
          <div class="left_items item">
            <span class="start">Live</span>
          </div>
          <div class="right_items item">
            <span class="accent">Better</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>


<script setup>
import { ref, onMounted, nextTick } from 'vue'
// import $gsap from '$gsap'
// import ScrollTrigger from '$gsap/ScrollTrigger'

// $gsap.registerPlugin(ScrollTrigger)
const { $gsap, $scrollTrigger } = useNuxtApp();



const sectionRef = ref(null)
// const titleRef = ref(null)
const descriptionRef = ref(null)

onMounted(async () => {
  if (process.server) return
  if (!$gsap || !$scrollTrigger) return


  const section = sectionRef.value
  const description = descriptionRef.value
  if (!description) return

  await nextTick()

  const lines = description.querySelectorAll('.line')
  if (!lines.length) return


  const isMobile = window.matchMedia('(max-width: 768px)').matches
  const startTrigger = isMobile ? 'top 85%' : 'bottom 70%'


  const tl = $gsap.timeline({
    scrollTrigger: {
      trigger: description,
      start: startTrigger,
      toggleActions: 'play none none none',
      once: true,
    },
  })

  tl.from(lines, {
    y: 40,
    opacity: 0,
    duration: 0.8,
    ease: 'power3.out',
    stagger: 0.25,
  })
})
</script>


// <!-- <script setup>
// import { onMounted, ref } from 'vue'
// import $gsap from '$gsap'
// import ScrollTrigger from '$gsap/ScrollTrigger'

// $gsap.registerPlugin(ScrollTrigger)

// // refs
// const sectionRef = ref(null)
// const titleRef = ref(null)
// const descriptionRef = ref(null)

// onMounted(() => {
//   const isDesktop = window.innerWidth > 700
//   const section = sectionRef.value
//   const description = descriptionRef.value
//   const lines = description?.querySelectorAll('.line') || []
//   const quoteTrigger = isDesktop ? 'bottom 70%' : 'top -45%'

//   const tl = $gsap.timeline({
//     scrollTrigger: {
//       trigger: description,
//       start: quoteTrigger,
//       toggleActions: 'play none none none',
//       once: true,
//     },
//   })


//   if (titleRef.value) {
//     tl.from(titleRef.value, {
//       y: 60,
//       opacity: 0,
//       duration: 1,
//       ease: 'power3.out',
//     })
//   }


//   lines.forEach((el, index) => {
//     tl.from(
//       el,
//       {
//         y: 40,
//         opacity: 0,
//         duration: 0.8,
//         delay: 0.3,
//         ease: 'power3.out',
//       },
//       '-=' + (0.4 + index * 0.2)
//     )
//   })
// })
// </script> -->




<style scoped lang="scss">

.quote {
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
  min-height: 100dvh;
  overflow: visible;
}

.quote::before {
  content: "";
  background-image: url("../images/quote-divider.png");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: top;
  position: absolute;
  overflow: hidden;
  display: flex;
  width: 100%;
  height: 2vh;
  top: 0;
}

.quote::after {
  content: "";
  background-image: url("../images/quote-divider.png");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: bottom;
  position: absolute;
  overflow: hidden;
  display: flex;
  width: 100%;
  height: 2vh;
  bottom: 0;
}

.quote_content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: auto;
  min-height: inherit;
  width: 100%;
  position: relative;

  .quote_text {
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    position: relative;
    transform: translateX(-40px);
    gap: 10px;

    @media screen and (max-width: 500px) {
      transform: translateX(-20px);
    }

    .line {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
    }

    span {
      color: #480074;
    }
    .accent {
      font-weight: 600;
      text-transform: uppercase;
    }
    .item {
      display: flex;
      flex-direction: column;
      align-items: center;
      flex: 1 0 100%;
    }
    .right_items {
      align-items: flex-start;
    }
    .left_items {
      align-items: flex-end;
    }
 
    span {
      font-size: clamp(32px, 5vw, 42px);

      @media screen and (max-width: 500px) {
        font-size: clamp(16px, 5vw, 32px);
      }
    }
  }
}




</style>