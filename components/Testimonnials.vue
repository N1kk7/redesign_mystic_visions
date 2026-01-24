<template>
  <section class="section testimonials" ref="sectionRef" id="testimonials">
    <div class="conntainer">
      <div class="image-wrapper">
        <NuxtImg
          src="/images/newsletter-1200.webp"
          sizes="(max-width: 480px) 480px, (max-width: 768px) 768px, 1200px"
          alt="book"
          style="width: 100%; height: auto;"
        />

        <div class="block-title">
          <h2>Testimonials</h2>
          <svg><use xlink:href="#arrow-right" /></svg>
        </div>
      </div>

      <div class="testimonials-wrapper" ref="testimonialsWrapperRef">
        <Swiper
          :modules="modules"
          :spaceBetween="30"
          :pagination="{ clickable: true }"
          :breakpoints="{
            0: { slidesPerView: 1 },
            768: { slidesPerView: 2 }
          }"
          class="mySwiper"
        >
          <SwiperSlide v-for="(slide, index) in slides" :key="index">
            <p class="block-description">
              {{ slide.text }}
              <br />
              <span class="author">{{ slide.author }}</span>
            </p>
          </SwiperSlide>
        </Swiper>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, nextTick } from 'vue'
import { Swiper, SwiperSlide } from 'swiper/vue'
import { Navigation, Pagination } from 'swiper/modules'
// import $gsap from '$gsap'
// import ScrollTrigger from '$gsap/ScrollTrigger'


// $gsap.registerPlugin(ScrollTrigger)
const { $gsap, $scrollTrigger } = useNuxtApp();


const sectionRef = ref(null)
const testimonialsWrapperRef = ref(null)
const modules = [Navigation, Pagination]

const slides = [
  {
    text: `I went from a directionless and anxious, 28-year-old man, to someone
    with a proper plan of action in just a few short months. I now have
    a newfound love for the gym from the tangible results of this
    consulting. And my relationships, both professional and personal,
    have been decoded and unobscured by all the psychological insights
    I've gained. The Mystic Visions consulting program is some of the
    best money I’ve ever spent, and the only way is up for me here on
    out.`,
    author: 'Anthony M',
  },
  {
    text: `I don’t really look at myself the same way as before I started the
    consulting. I would highly recommend it for those who are struggling
    with obstacles that keep them from moving forward. During
    consulting, there has never been a time where I presented a problem
    and it wasn’t met with a solution...`,
    author: 'Liam S',
  },
  {
    text: `Pillars presents a robust study in how to make it in life, replete
    with résumé tips, fitness and supplement information, sex magick,
    and yes, political commentary...`,
    author: 'Ancient Problemz',
  },
  {
    text: `GLO’s prose is lively and engaging, his practical advice useful and
    actionable, and his broader narrative sophisticated and compelling...`,
    author: 'Walt Bismarck',
  },
  {
    text: `It’s easy to see this book as primarily removing pillars of folly,
    like blind Samson in the enemy temple...`,
    author: 'Rach',
  },
]


onMounted(async () => {
  if (process.server) return 
  if (!$gsap || !$scrollTrigger) return


  const testimonialsWrapper = testimonialsWrapperRef.value
  if (!testimonialsWrapper) return

  await nextTick()

  const testimonials = testimonialsWrapper.querySelectorAll('.swiper-slide p')
  if (!testimonials.length) return

  const isMobile = window.matchMedia('(max-width: 768px)').matches
  const startTrigger = isMobile ? 'top 90%' : 'bottom 95%'

  const tl = $gsap.timeline({
    scrollTrigger: {
      trigger: testimonialsWrapper,
      start: startTrigger,
      toggleActions: 'play none none none',
      once: true,
    },
  })

  tl.from(testimonials, {
    y: 60,
    opacity: 0,
    duration: 1,
    ease: 'power2.out',
    stagger: 0.3,
  })
})
</script>




// <!-- <script setup >

// import { ref, onMounted, nextTick } from 'vue'
// import $gsap from '$gsap'
// import ScrollTrigger from '$gsap/ScrollTrigger'

// import { Swiper, SwiperSlide } from 'swiper/vue';
// import { Navigation, Pagination } from 'swiper/modules';

// const modules = [Navigation, Pagination];


// $gsap.registerPlugin(ScrollTrigger)

// const sectionRef = ref(null)
// const testimonialsWrapperRef = ref(null)


// const slides = [
//   {
//     text: `I went from a directionless and anxious, 28-year-old man, to someone
//     with a proper plan of action in just a few short months. I now have
//     a newfound love for the gym from the tangible results of this
//     consulting. And my relationships, both professional and personal,
//     have been decoded and unobscured by all the psychological insights
//     I've gained. The Mystic Visions consulting program is some of the
//     best money I’ve ever spent, and the only way is up for me here on
//     out.`,
//     author: 'Anthony M',
//   },
//   {
//     text: `I don’t really look at myself the same way as before I started the
//     consulting. I would highly recommend it for those who are struggling
//     with obstacles that keep them from moving forward. During
//     consulting, there has never been a time where I presented a problem
//     and it wasn’t met with a solution...`,
//     author: 'Liam S',
//   },
//   {
//     text: `Pillars presents a robust study in how to make it in life, replete
//     with résumé tips, fitness and supplement information, sex magick,
//     and yes, political commentary...`,
//     author: 'Ancient Problemz',
//   },
//   {
//     text: `GLO’s prose is lively and engaging, his practical advice useful and
//     actionable, and his broader narrative sophisticated and compelling...`,
//     author: 'Walt Bismarck',
//   },
//   {
//     text: `It’s easy to see this book as primarily removing pillars of folly,
//     like blind Samson in the enemy temple...`,
//     author: 'Rach',
//   },
// ];




// onMounted(async () => {
//   const isDesktop = window.innerWidth > 700
//   const testimonialsWrapper = testimonialsWrapperRef.value

//   await nextTick()


//   const testimonials = testimonialsWrapper?.querySelectorAll('.swiper-slide p') || []
//   const startTestimonials = isDesktop ? 'bottom 95%' : 'top -10%'

//   if (testimonials.length) {
//     const tl = $gsap.timeline({
//       scrollTrigger: {
//         trigger: testimonials[0],
//         start: startTestimonials,
//         toggleActions: 'play none none none',
//         once: true,
//       },
//     })

//     tl.from(testimonials, {
//       y: 60,
//       opacity: 0,
//       duration: 1,
//       ease: 'power2.out',
//       stagger: 0.3,
//     })
//   }
// })



// </script> -->



<style scoped lang="scss">


.testimonials{
    .image-wrapper{
        position: relative;
        margin-bottom: 50px;
        img{
          width: 100%;
          height: 70vh !important;
          object-fit: cover;
        }
        
    }
}


.block-title{
    width: fit-content;
    min-width: 45%;
    height: fit-content;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #fff;
    position: absolute;
    padding: 20px 15px 10px;
  
    bottom: 0;
    left: 0;
    .text{
        display: flex;
        flex-direction: column;
        gap: 10px;

    
    }
    .after-title{
        display: flex;
        flex-direction: column;
    }
    h2{
        font-weight: 500;
        font-size: clamp(18px, 2.5vw, 42px);
    }
    span{
        color: #7A70FF;
        font-size: clamp(18px, 2.5vw, 42px);
    }
     svg{
        border: 1px solid #5b50d8;
        border-radius: 50%;
        fill: #5b50d8;
        padding: 5px;
        width: 40px;
        height: 40px;
      }
      @media screen and (min-width: 1024px) {
        &:hover{
          background-color: #5b50d8;
          transition: all ease 0.3s;
          h2{
            color: white;

          }
          span{
            color: white;
          }
          svg{
            border: 1px solid white;
            fill: white;
          }
        }
      }
      @media screen and (max-width: 768px) {
        display: none;
        
      }
}

.testimonials-wrapper{
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    position: relative;
    gap: 2vw;
    p{
      flex: 1;
    }
    @media screen and (max-width: 650px) {
        flex-direction: column;
        
    }

    .author{
      display: block;
      text-align: end;
      margin-top: 10px;
      width: 100%;
    }

    
}



</style>