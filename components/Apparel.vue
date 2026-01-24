
<template>
  <section ref="section" class="apparel section animate-content" id="apparel">
    <div class="conntainer">
      <div class="block_content_wrapper">
        <div class="img_conntainer" ref="imgContainer">
          <NuxtImg
            src="/images/apparel-1200.webp"
            sizes="(max-width: 480px) 480px, (max-width: 768px) 768px, 1200px"
            alt="apparel"
            style="width: 100%; height: auto;"
          />
          <a
            href="https://shop.thepillarsofwisdom.com/collections/all"
            target="_blank"
            class="link-element"
          >
            <h2>Mystic Merch</h2>
            <svg>
              <use xlink:href="#arrow-right"></use>
            </svg>
          </a>

          <div class="mobile_content">
            <h2 class="mobile_title">
              Wear Your Intent: <br />
              Curated Essentials
            </h2>
          </div>
        </div>

        <div class="info_content">
          <h2 ref="title" class="block_title">
            Wear Your Intent: <br />
            Curated Essentials
          </h2>

          <p ref="desc" class="block-description">
            Forge your identity with apparel that screams defiance. Our exclusive
            Pillars of Wisdom collection isn’t just gear; it’s a badge for the
            elite who reject the system’s chains. Crafted for visionaries, each
            piece embodies the raw power of Nietzschean will and the edge of
            schizoanalysis. Stand out, stay bold, and wear your rebellion. Shop
            now and join the brotherhood that dominates.
          </p>

          <a
            ref="button"
            href="https://shop.thepillarsofwisdom.com/collections/all"
            target="_blank"
            class="link-btn"
          >
            Claim Your Badge
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
const imgContainer = ref(null)
const title = ref(null)
const desc = ref(null)
const button = ref(null)

onMounted(() => {
  if (!section.value) return
  if (!$gsap || !$scrollTrigger) return

  const titleEl = title.value
  const originalText = titleEl.textContent.trim()
  titleEl.textContent = ''
  const words = originalText.split(' ');

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
      start: 'top 60%',
      toggleActions: 'play none none none',
      once: true,
    },
  })

  tl.from(imgContainer.value, {
    xPercent: -40,
    opacity: 0,
    duration: 0.8,
    ease: 'power3.out',
  })

  tl.from(titleEl.querySelectorAll('.line'), {
    y: 60,
    opacity: 0,
    duration: 0.6,
    ease: 'power3.out',
    stagger: 0.2,
  }, '-=0.3')

  tl.from(desc.value, {
    y: 80,
    opacity: 0,
    duration: 1,
    ease: 'power3.out',
  }, '-=0.2')

  $gsap.set(button.value, { opacity: 0, y: 20 })
  tl.to(button.value, {
    opacity: 1,
    y: 0,
    duration: 0.5,
    ease: 'power2.out',
  }, '-=0.3')
})
</script>



<style scoped lang="scss">

.apparel {
  .link-element {
    right: 0;
    left: unset !important;
  }

  @media screen and (min-width: 768px) {
    .block_content_wrapper {
      justify-content: center;
    }
  }
  @media screen and (max-width: 768px) {
    .mobile_content {
      justify-content: flex-end !important;
      h2 {
        text-align: justify;
      }
    }
  }

  @media screen and (min-width: 768px) {
    .img_conntainer {
      flex: 0 0 50% !important;
    }
    .info_content {
      flex: 0 0 35% !important;

      .block-description {
        font-size: clamp(19px, 1.2vw, 24px);
        margin: 0 auto;
      }

      a {
        margin: 0 auto;

        width: -webkit-fill-available;
        white-space: nowrap;
      }
    }
  }
}




</style>