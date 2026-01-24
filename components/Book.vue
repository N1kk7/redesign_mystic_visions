
<template>
  <section ref="section" class="newsletter section animate-content" id="book">
    <div class="conntainer">
      <div class="block_content_wrapper">
        <div class="info_content">
          <div class="title_content">
            <h2 ref="title" class="block_title">
              Join the Elite:
              <br />
              Own The Pillars of Wisdom and Rise Above the Rest.
            </h2>
          </div>

          <p ref="firstDesc" class="block-description">
            This isn’t just a book—it’s your ticket to the inner circle of
            visionaries who refuse to be chained by ordinary thinking.
            <span class="accent-text">The Pillars of Wisdom</span> arms you with
            the raw, unfiltered truths about liberalism, modernity, stoicism,
            economics, and more, dissected with a fearless edge that separates
            the bold from the herd. By owning this book, you’re not just
            reading—you’re claiming your place among the enlightened few who
            dare to master their destiny. Reclaim the bold legacy of great
            minds, wield psychoanalytic insights to conquer the world’s psyche,
            and harness schizoanalysis to shatter societal shackles. This is
            your blueprint to dominate, whether it’s through
            location-independent wealth, geo-arbitrage, or a life of unmatched
            purpose.
          </p>

          <div class="list_wrapper">
            <h3 ref="listTitle" class="list_title">Why You Need This Now</h3>

            <ul ref="listItems" class="text_list">
              <li>
                <h4>Stand Apart</h4>
                <p>Possess knowledge that elevates you above the masses.</p>
              </li>
              <li>
                <h4>Exclusive Access</h4>
                <p>
                  Join a rare community of high-achievers who own this
                  provocative masterpiece.
                </p>
              </li>
              <li>
                <h4>Seize Control</h4>
                <p>
                  Learn to outsmart systems and use the economy to build a
                  legacy of power.
                </p>
              </li>
              <li>
                <h4>Act Fast</h4>
                <p>
                  With censorship looming, this is your chance to secure the
                  uncensored hardcover.
                </p>
              </li>
            </ul>
          </div>

          <p ref="lastDesc" class="block-description">
            Don’t settle for mediocrity. Grab
            <span class="accent-text">The Pillars of Wisdom</span>
            today and become part of the select few who live extraordinary
            lives.
          </p>

          <a
            ref="button"
            href="https://shop.thepillarsofwisdom.com/cart/49305684803752:1"
            target="_blank"
            class="link-btn"
          >
            Grab Your Copy
          </a>
        </div>

        <div class="img_conntainer" ref="imgContainer">
          <NuxtImg
            src="/images/book-final-1200.webp"
            sizes="(max-width: 480px) 480px, (max-width: 768px) 768px, 1200px"
            alt="book"
            style="width: 100%; height: auto;"
          />
          <a
            href="https://shop.thepillarsofwisdom.com/cart/49305684803752:1"
            target="_blank"
            class="link-element"
          >
            <h2>Book</h2>
            <svg><use xlink:href="#arrow-right"></use></svg>
          </a>

          <div class="mobile_content">
            <h2 class="mobile_title">
              Join the Elite: Own The Pillars of Wisdom and Rise Above the Rest.
            </h2>
          </div>
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
const imgContainer = ref(null)
const firstDesc = ref(null)
const lastDesc = ref(null)
const listTitle = ref(null)
const listItems = ref(null)
const button = ref(null)

onMounted(() => {
  if (!section.value) return
    if (!$gsap || !$scrollTrigger) return
  

  const isDesktop = window.innerWidth > 700
  const startTrigger = isDesktop ? 'top 55%' : 'top 50%'


  const titleEl = title.value
  const originalText = titleEl.textContent.trim()
  titleEl.textContent = ''
  const words = originalText.split(' ')

  words.forEach(word => {
    const span = document.createElement('span')
    span.classList.add('word')
    span.textContent = word + ' '
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
      start: startTrigger,
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


  tl.from(titleEl.querySelectorAll('.line'), {
    y: 60,
    opacity: 0,
    duration: 0.6,
    ease: 'power3.out',
    stagger: 0.2,
  }, '-=0.3')


  if (firstDesc.value) {
    tl.from(firstDesc.value, {
      y: 200,
      opacity: 0,
      duration: 1,
      ease: 'power3.out',
    }, '-=0.2')
  }


  if (listTitle.value) {
    tl.from(listTitle.value, {
      y: 40,
      opacity: 0,
      duration: 0.8,
      ease: 'power3.out',
    }, '-=0.4')
  }


  if (listItems.value) {
    const li = listItems.value.querySelectorAll('li')
    tl.from(li, {
      y: 40,
      opacity: 0,
      duration: 0.6,
      ease: 'power2.out',
      stagger: 0.2,
    }, '-=0.5')
  }


  if (lastDesc.value) {
    tl.from(lastDesc.value, {
      y: 160,
      opacity: 0,
      duration: 1,
      ease: 'power3.out',
    }, '-=0.2')
  }


  if (button.value) {
    $gsap.set(button.value, { opacity: 0, y: 20 })
    tl.to(button.value, {
      opacity: 1,
      y: 0,
      duration: 0.5,
      ease: 'power2.out',
    }, '-=0.3')
  }
})
</script>



<style scoped lang="scss">

.newsletter {
  .block_content_wrapper {
    .title_content {
      align-items: end;
      margin-right: auto;
    }
    @media screen and (max-width: 768px) {
      flex-direction: column-reverse;
    }
  }
  .link-element {
    transform: translate(-1px, 1px);
    z-index: 5;
  }
  .info_content {
    align-items: end;

    @media screen and (max-width: 768px) {
      align-items: start;
    }
  }
  @media screen and (max-width: 768px) {
    .mobile_content {
      justify-content: flex-end !important;
    }
  }
}



</style>


