<!-- <template>
  <section class="reviews" ref="reviewsRef">
    <div class="container">
      <div class="reviews_content">
        <div
          class="reviews_content_item"
          v-for="(item, i) in reviewData"
          :key="i"
          :ref="setCardRef"
        >
          <div class="card_top">
            <NuxtImg
              class="reviews_content_item_avatar"
              :src="item.avatar"
              :alt="item.author"
              width="50"
              height="50"
            />
            <p v-html="item.text"></p>
          </div>
          <div class="card_bottom">
            <strong>{{ item.author }}</strong>
            <div class="card_position">{{ item.position }}</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<!-- <script setup>
import { ref, onMounted, onBeforeUpdate, nextTick } from "vue";

import gsap from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const reviewsRef = ref(null);
const titleRef = ref(null);
const cardRefs = ref([]);

const reviewData = [
  {
    avatar: "/images/liam_s.webp",
    text: `"<strong>Before this, I had no clear structure.</strong> I knew I wanted to lower costs, work remotely, and change my living situation, but I didn't know how to organize those goals."`,
    author: "Liam S.",
    position: "Remote Software Engineer — United States",
  },
  {
    avatar: "/images/sean_m.webp",
    text: `"What stood out most was how my thinking changed. <strong>The ideas weren't abstract.</strong> They helped me see my situation more clearly and make better decisions."`,
    author: "Sean M.",
    position: "Independent Consultant — United States",
  },
  {
    avatar: "/images/alexander_k.webp",
    text: `"I didn't need more motivation. <strong>I needed to place my effort correctly.</strong> Once I understood that, my decisions became simpler and my actions more deliberate."`,
    author: "Alexander K.",
    position: "Product & Operations Manager — Germany",
  },
];

const setCardRef = (el) => {
  if (el) cardRefs.value.push(el);
};

onBeforeUpdate(() => {
  cardRefs.value = [];
});

onMounted(async () => {

  await nextTick();

  const isDesktop = window.innerWidth >= 768;

  gsap.from(titleRef.value, {
    x: -100,
    opacity: 0,
    duration: 1,
    ease: "power4.out",
    scrollTrigger: {
      trigger: titleRef.value,
      start: "top 80%",
      once: true,
    },
  });

  if (isDesktop) {
    gsap.from(cardRefs.value, {
      y: 60,
      opacity: 0,
      duration: 0.8,
      stagger: 0.25,
      ease: "power3.out",
      scrollTrigger: {
        trigger: cardRefs.value[0],
        start: "top 85%",
        once: true,
      },
    });
  } else {
    cardRefs.value.forEach((el) => {
      gsap.from(el, {
        x: -50,
        opacity: 0,
        duration: 0.7,
        ease: "power3.out",
        scrollTrigger: {
          trigger: el,
          start: "top 90%",
          once: true,
        },
      });
    });
  }
});
</script> -->


<!-- <script setup>
import { onMounted, ref, nextTick } from "vue";
import gsap from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const reviewData = [
  {
    avatar: "/images/liam_s.webp",
    text: `"<strong>Before this, I had no clear structure.</strong> I knew I wanted to lower costs, work remotely, and change my living situation, but I didn't know how to organize those goals."`,
    author: "Liam S.",
    position: "Remote Software Engineer — United States",
  },
  {
    avatar: "/images/sean_m.webp",
    text: `"What stood out most was how my thinking changed. <strong>The ideas weren't abstract.</strong> They helped me see my situation more clearly and make better decisions."`,
    author: "Sean M.",
    position: "Independent Consultant — United States",
  },
  {
    avatar: "/images/alexander_k.webp",
    text: `"I didn't need more motivation. <strong>I needed to place my effort correctly.</strong> Once I understood that, my decisions became simpler and my actions more deliberate."`,
    author: "Alexander K.",
    position: "Product & Operations Manager — Germany",
  },
];

const reviewsRef = ref(null);

onMounted(async () => {
  await nextTick();

  const section = reviewsRef.value;
  if (!section) return;

  const cards = section.querySelectorAll(".reviews_content_item");

  gsap.timeline({
    scrollTrigger: {
      trigger: section,
      start: "top 80%",
      toggleActions: "play none none none",
    },
  })
    .to(cards, {
      y: 0,
      scale: 1,
      opacity: 1,
      duration: 0.8,
      ease: "power3.out",
      stagger: 0.2,
    });
});
</script> --> 
<template>
  <section class="reviews" ref="reviewsRef">
    <div class="container">
      <div class="reviews_content">
        <!-- Карточка 1 -->
        <div class="reviews_content_item" ref="card1">
          <div class="card_top">
            <div class="reviews_content_item_avatar_wrapper">
                <NuxtImg
                    class="reviews_content_item_avatar"
                    src="/images/liam_s.webp"
                    alt="Liam S."
                    width="50"
                    height="50"
                />
            </div>
            <!-- <NuxtImg
              class="reviews_content_item_avatar"
              src="/images/liam_s.webp"
              alt="Liam S."
              width="50"
              height="50"
            /> -->
            <p>
              "<strong>Before this, I had no clear structure.</strong> I knew I wanted to lower costs, work remotely, and change my living situation, but I didn't know how to organize those goals."
            </p>
          </div>
          <div class="card_bottom">
            <strong>Liam S.</strong>
            <div class="card_position">Remote Software Engineer — United States</div>
          </div>
        </div>

        <!-- Карточка 2 -->
        <div class="reviews_content_item" ref="card2">
          <div class="card_top">
            <div class="reviews_content_item_avatar_wrapper">

                 <NuxtImg
                    class="reviews_content_item_avatar"
                    src="/images/sean_m.webp"
                    alt="Sean M."
                    width="50"
                    height="50"
                    />


            </div>

           
            <p>
              "What stood out most was how my thinking changed. <strong>The ideas weren't abstract.</strong> They helped me see my situation more clearly and make better decisions."
            </p>
          </div>
          <div class="card_bottom">
            <strong>Sean M.</strong>
            <div class="card_position">Independent Consultant — United States</div>
          </div>
        </div>

        <!-- Карточка 3 -->
        <div class="reviews_content_item" ref="card3">
          <div class="card_top">
            <div class="reviews_content_item_avatar_wrapper">

<NuxtImg
              class="reviews_content_item_avatar"
              src="/images/alexander_k.webp"
              alt="Alexander K."
              width="50"
              height="50"
            />
            </div>
            
            
            <p>
              "I didn't need more motivation. <strong>I needed to place my effort correctly.</strong> Once I understood that, my decisions became simpler and my actions more deliberate."
            </p>
          </div>
          <div class="card_bottom">
            <strong>Alexander K.</strong>
            <div class="card_position">Product & Operations Manager — Germany</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, nextTick } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const reviewsRef = ref(null);
const card1 = ref(null);
const card2 = ref(null);
const card3 = ref(null);

onMounted(async () => {
  await nextTick();

  const cards = [card1.value, card2.value, card3.value];

  // Сначала делаем все opacity 0 через CSS (или через JS)
  cards.forEach((card) => {
    card.style.opacity = 0;
    card.style.transform = "translateY(40px) scale(0.95)";
  });

  // Ждём загрузки картинок
  const images = document.querySelectorAll(".reviews_content_item_avatar");
  await Promise.all(
    Array.from(images).map(
      (img) =>
        img.complete
          ? Promise.resolve()
          : new Promise((res) => (img.onload = res))
    )
  );

  const isDesktop = window.innerWidth >= 768;

  if (isDesktop) {
    gsap.to(cards, {
      y: 0,
      scale: 1,
      opacity: 1,
      duration: 0.8,
      ease: "power3.out",
      stagger: 0.25,
      scrollTrigger: {
        trigger: reviewsRef.value,
        start: "top 80%",
        toggleActions: "play none none none",
      },
    });
  } else {
    cards.forEach((card) => {
      gsap.to(card, {
        y: 0,
        scale: 1,
        opacity: 1,
        duration: 0.7,
        ease: "power3.out",
        scrollTrigger: {
          trigger: card,
          start: "top 90%",
          toggleActions: "play none none none",
        },
      });
    });
  }
});
</script>

<style lang="scss">

    .reviews {
        width: 100%;
        height: auto;
        position: relative;
        padding-block: 128px;


        &_content {
            display: grid;
            // grid-template-columns: repeat(3, 1fr);
            grid-template-columns: repeat(3, minmax(0, 1fr));
            align-items: stretch;
            gap: 48px;




            &_item {
                box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
                  opacity: 0;
                    transform: translateY(40px) scale(0.95);
                display: flex;
                flex-direction: column;
                justify-content: space-between;
                align-items: center;
                border: 1px solid #d4d4db;
                border-radius: 22px;
                padding: 32px;
                gap: 24px;

                &_avatar_wrapper {
                    width: 96px;
                    height: 96px;
                    border-radius: 50%;
                    border: 4px solid #7033ff;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    // object-fit: cover;
                    overflow: hidden;
                    position: relative;

                    img {
                        width: 100%;
                        height: 100%;
                        object-fit: cover;
                    }
                    
                }

                @media screen and (max-width: 768px) {
                    box-sizing: border-box;
                    width: 100%;
                }
            }

            @media screen and (max-width: 1024px) {
                gap: clamp(10px, 3vw, 48px);
            }

            @media screen and (max-width: 768px) {
                display: flex;
                flex-direction: column;
                justify-content: flex-start;
                align-items: center;
                gap: 24px;
            }
        }

        .card_top {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            gap: 24px;

            p {
                font-family: "Roboto", sans-serif;
                font-size: 1rem;
                line-height: 150%;
                font-weight: 400;
                font-style: normal;
            }
        }

        .card_bottom {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            gap: 5px;

            .card_author {
                 font-family: "Roboto", sans-serif;
                font-size: 1rem;
                line-height: 150%;
                font-weight: 500;
                font-style: normal;
            }

            .card_position {
                 font-family: "Roboto", sans-serif;
                font-size: 0.8rem;
                line-height: 150%;
                font-weight: 400;
                font-style: normal;
                text-align: center;
            }

            
        }
        .card_position {
                font-size: .85rem;
                font-weight: 400;
            }


        @media screen and (max-width: 1024px) {
            padding-block: 100px;

        }

        @media screen and (max-width: 768px) {
            padding-block: 90px;
        }

        @media screen and (max-width: 425px) {
            padding-block: 75px;
        }

        @media screen and (max-width: 375px) {
            padding-block: 60px;
        }
 








    }



</style>
