<template>
  <section ref="section" class="coaching section animate-content" id="consulting">
    <div ref="coachingImages" class="coaching_images">
      <NuxtImg
        src="/images/filled-figure.webp"
        width="1200"
        height="800"
        alt="figure"
        class="left-img figure-img"
      />

      <NuxtImg
        src="/images/transparent-figure.webp"
        width="1200"
        height="800"
        alt="figure"
        class="right-img figure-img"
      />
    </div>

    <div class="conntainer">
      <div class="block_content_wrapper">
        <div class="info_content">
          <h2 ref="title" class="block_title">
            Seize Your Destiny:<br />
            Join the Elite with Our Exclusive Consulting Program
          </h2>

          <p ref="firstDesc" class="block-description">
            This isn’t just consulting—it’s your key to joining a rare brotherhood
            of visionaries who reject mediocrity and claim their place at the top.
            <span class="accent-text">The Pillars of Wisdom</span> is your guide,
            and our exclusive consulting program is your catalyst...
          </p>

          <div class="list_wrapper">
            <h3 ref="listTitle" class="list_title">Why Join Now?</h3>

            <ul ref="list" class="text_list">
              <li>
                <h4>Rise Above</h4>
                <p class="block-description">
                  Gain knowledge that sets you apart from the ordinary.
                </p>
              </li>
              <li>
                <h4>Exclusive Brotherhood</h4>
                <p class="block-description">
                  Become part of a high-caliber community of men who live
                  extraordinary lives.
                </p>
              </li>
              <li>
                <h4>Command Your Future</h4>
                <p>Learn to conquer the economy and forge a legacy of power.</p>
              </li>
              <li>
                <h4>Act Before It's Too Late</h4>
                <p class="block-description">
                  Limited spots remain—secure your place in our elite program today.
                </p>
              </li>
            </ul>
          </div>

          <p ref="lastDesc" class="block-description">
            Don’t settle for average. Enroll now and claim your rightful place
            among the unstoppable.
          </p>

          <a href="/pages/coaching.html" ref="button" class="link-btn">
            Secure Your Spot
          </a>
        </div>

        <div class="img_conntainer" ref="imgContainer">
          <NuxtImg
            src="/images/coaching-1200.webp"
            sizes="(max-width: 480px) 480px, (max-width: 768px) 768px, 1200px"
            alt="book"
            style="width: 100%; height: auto;"
          />

          <a href="/pages/coaching.html" class="link-element">
            <h2>Consulting</h2>
            <svg><use xlink:href="#arrow-right"></use></svg>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>


<script setup>
import { ref, onMounted } from 'vue'
// import $gsap from '$gsap'
// import ScrollTrigger from '$gsap/ScrollTrigger'

// $gsap.registerPlugin(ScrollTrigger)
const { $gsap, $scrollTrigger } = useNuxtApp();


const section = ref(null)
const title = ref(null)
const coachingImages = ref(null)
const imgContainer = ref(null)
const firstDesc = ref(null)
const lastDesc = ref(null)
const listTitle = ref(null)
const list = ref(null)
const button = ref(null)

onMounted(() => {
  if (!section.value) return
  if (!$gsap || !$scrollTrigger) return


  const leftImg = coachingImages.value.querySelector('.left-img')
  const rightImg = coachingImages.value.querySelector('.right-img')


  const titleEl = title.value
  const originalText = titleEl.textContent.trim()
  titleEl.textContent = ''
  const words = originalText.split(' ')


  words.forEach(word => {
    const span = document.createElement('span')
    span.classList.add('word')
    span.innerHTML = word + ' '
    titleEl.appendChild(span)
  })


  const wordEls = Array.from(titleEl.querySelectorAll('.word'))
  const lines = []
  let currentTop = null
  let currentLine = []

  wordEls.forEach(el => {
    const top = el.getBoundingClientRect().top
    if (currentTop === null || Math.abs(top - currentTop) < 2) {
      currentLine.push(el)
      currentTop = top
    } else {
      lines.push(currentLine)
      currentLine = [el]
      currentTop = top
    }
  })
  if (currentLine.length) lines.push(currentLine)
  lines.forEach(lineWords => {
    const lineWrapper = document.createElement('div')
    lineWrapper.classList.add('line')
    lineWords[0].parentNode.insertBefore(lineWrapper, lineWords[0])
    lineWords.forEach(word => lineWrapper.appendChild(word))
  })


  const tl = $gsap.timeline({
    scrollTrigger: {
      trigger: section.value,
      start: 'top 55%',
      toggleActions: 'play none none none',
      once: true,
    },
  })

  tl.from(imgContainer.value, {
      xPercent: 40,
    opacity: 0,
    duration: 0.8,
    ease: 'power3.out',
  })


  tl.from(leftImg, { xPercent: -100, opacity: 0, duration: 0.8, ease: 'power3.out' })
  tl.from(rightImg, { xPercent: 100, opacity: 0, duration: 0.8, ease: 'power3.out' }, '<')

  tl.from(titleEl.querySelectorAll('.line'), {
    y: 60,
    opacity: 0,
    duration: 0.6,
    ease: 'power3.out',
    stagger: 0.2,
  })

  

  tl.from(firstDesc.value, { y: 300, opacity: 0, duration: 1, ease: 'power3.out' }, '-=0.2')

  

  tl.from(listTitle.value, { y: 40, opacity: 0, duration: 0.8, ease: 'power3.out' }, '-=0.4')

  tl.from(list.value.querySelectorAll('li'), {
    y: 40,
    opacity: 0,
    duration: 0.6,
    ease: 'power2.out',
    stagger: 0.2,
  }, '-=0.5')

  tl.from(lastDesc.value, { y: 160, opacity: 0, duration: 1, ease: 'power3.out' }, '-=0.2')

  $gsap.set(button.value, { opacity: 0, y: 20 })
  tl.to(button.value, { opacity: 1, y: 0, duration: 0.5, ease: 'power2.out' }, '-=0.3')
})
</script>



<style scoped lang="scss">
.coaching {
  .link-element {
    transform: translate(-1px, 1px);
    z-index: 5;
  }

  .coaching_images {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;

    .figure-img {
      width: 350px;
      height: 100%;
      @media screen and (max-width: 768px) {
        width: 215px;
        height: 50%;
      }
    }
    .left-img {
      position: absolute;
      left: -185px;
      top: 0;
      @media screen and (max-width: 768px) {
        left: -85px;
      }
    }
    .right-img {
      position: absolute;
      right: -185px;
      top: 0;
      @media screen and (max-width: 768px) {
        right: -85px;
      }
    }
  }


  .info_content {
    align-items: start;
  }
  h2 {
    line-height: 38px;
    font-weight: 600;
  }
  .block_subtitle {
    font-size: clamp(20px, 1.2vw, 30px);
    font-weight: 400;
  }
  .button_group {
    padding-top: 70px;
    position: relative;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    align-items: center;
    gap: 25px;
    button {
      flex: 1;
      white-space: nowrap;
    }
  }

  @media screen and (max-width: 768px) {
    .block_content_wrapper {
      flex-direction: column-reverse;
    }
  }

  @media screen and (min-width: 768px) {
    .link-btn {
      margin-left: auto;
    }
  }

  .coaching_tags {
    padding-top: 30px;
  }
  @media screen and (max-width: 768px) {
    .block_title {
      display: none;
    }
    .mobile_content {
      justify-content: flex-end !important;
      h2 {
        text-align: justify;
      }
    }
  }
}



</style>