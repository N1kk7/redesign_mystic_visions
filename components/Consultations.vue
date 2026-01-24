<template>
  <section ref="sectionRef" class="section consultations" id="consulting">
    <div class="consultations_content">
      <div class="images_content">
        <img
          ref="leftImgRef"
          src="/images/sphinks-1200.webp"
          width="1200"
          height="1125"
          alt="sphinks"
          class="left-img sphinks-img"
        />
        <img
          ref="rightImgRef"
          src="/images/sphinks-1200.webp"
          width="1200"
          height="1125"
          alt="sphinks"
          class="right-img sphinks-img"
        />
      </div>

      <div class="text_content">
        <h2 ref="headingRef">Book a consultation</h2>
        <p ref="paragraphRef">
          Ready to see through the illusions and dominate the world? Book a
          consultation now to unlock the raw, unfiltered truths of
          <span class="accent-text">The Pillars of Wisdom</span> and join the
          exclusive elites who reject the system’s lies. Master your will to
          power, build unshakable wealth, and live life on your terms—starting
          with this one bold move. Spots are limited, and the ordinary will be
          left behind. Seize your place among the elite—act now!
        </p>
        <button
          class="link-btn"
          ref="buttonRef"
          @click="modalStore.showModal('ModalMain')"
        >
          Secure Your Spot
        </button>
      </div>
    </div>
  </section>
</template>


<script setup>
import { ref, onMounted, nextTick } from 'vue'
// import $gsap from '$gsap'
// import ScrollTrigger from '$gsap/ScrollTrigger'



const sectionRef = ref(null)
const leftImgRef = ref(null)
const rightImgRef = ref(null)
const headingRef = ref(null)
const paragraphRef = ref(null)
const buttonRef = ref(null)

const modalStore = useModalStore()

onMounted(async () => {
  if (process.server) return

  await nextTick()
  const { $gsap, $ScrollTrigger } = useNuxtApp();

  // $gsap.registerPlugin(ScrollTrigger)

  const section = sectionRef.value
  if (!section) return

  const isMobile = window.innerWidth > 700
  const startTrigger = isMobile ? 'top 60%' : 'bottom 90%'

  const tl = $gsap.timeline({
    scrollTrigger: {
      trigger: section,
      start: startTrigger,
      toggleActions: 'play none none none',
      once: true,
    },
  })

  if (leftImgRef.value) {
    tl.from(leftImgRef.value, {
      xPercent: -100,
      opacity: 0,
      duration: 1.2,
      ease: 'power3.out',
    })
  }

  if (rightImgRef.value) {
    tl.from(
      rightImgRef.value,
      {
        xPercent: 100,
        opacity: 0,
        duration: 1.2,
        ease: 'power3.out',
      },
      '<'
    )
  }

  if (headingRef.value) {
    tl.from(headingRef.value, {
      y: 60,
      opacity: 0,
      duration: 1,
      ease: 'power3.out',
    })
  }

  if (paragraphRef.value) {
    tl.from(
      paragraphRef.value,
      {
        y: 40,
        opacity: 0,
        duration: 1,
        ease: 'power3.out',
      },
      '-=0.5'
    )
  }


  if (buttonRef.value) {
    $gsap.set(buttonRef.value, { opacity: 0, y: 30 })

    tl.to(
      buttonRef.value,
      {
        opacity: 1,
        y: 0,
        duration: 0.8,
        ease: 'power2.out',
      },
      '-=0.4'
    )
  }
})
</script>


<style lang="scss" scoped>

.consultations_content {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  h2{
    font-family: "SF-Pro", sans-serif;
    font-size: clamp(32px, 2.4vw, 42px);
    font-weight: 500;
    line-height: 1.2;
    color: #480074;
  }
  p {
    font-family: "SF-Pro", sans-serif;
    font-size: clamp(18px, 1.2vw, 24px);
    line-height: 1.2;
    font-weight: 400;
    color: #480074;
  }
  .accent-text {
      font-style: italic;
      font-weight: 900;
  }
}

.text_content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 30px;
  width: 50vw;
  z-index: 1;
  h2 {
    width: 100%;
  }
  @media screen and (max-width: 1024px) {
    width: 42vw;
  }

  @media screen and (max-width: 768px) {
    width: 50vw;
  }

  @media screen and (max-width: 600px) {
    width: 55vw;
  }

  @media screen and (max-width: 500px) {
    width: 60vw;
  }

  p {
    text-align: justify;
  }
}

.images_content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: absolute;
  padding-inline: 5vw;
  width: 100%;
  height: 100%;
  @media screen and (max-width: 1024px) {
    padding-inline: 2vw;
  }

  @media screen and (max-width: 768px) {
    padding-inline: 0;
    width: 120%;
  }

  @media screen and (max-width: 600px) {
    width: 135%;
  }

  @media screen and (max-width: 500px) {
    width: 160%;
  }
  @media screen and (max-width: 400px) {
    width: 180%;
  }
  @media screen and (max-width: 350px) {
    width: 190%;
  }
}

.sphinks-img {
  width: 200px;
  height: 200px;
}

.right-img {
  transform: scaleX(-1);
}

.link-btn {
	background: #5b50d8;
	font-family: "SF-Pro", sans-serif;
  font-weight: 600;
	border: 1px solid transparent;
	border-radius: 50px;
	padding: 15px 30px;
	color: #fff;
	text-align: center;
	cursor: pointer;
	width: -moz-fit-content;
	width: fit-content;
	transition: all ease 0.3s;
}
@media screen and (min-width: 1024px) {
	.link-btn:hover {
		border: 1px solid #5b50d8;
		background-color: #443f8b;
		transition: all ease 0.3s;
	}
}
@media screen and (max-width: 768px) {
	.link-btn {
		width: -webkit-fill-available;
	}
}




</style>
