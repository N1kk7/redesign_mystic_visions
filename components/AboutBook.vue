<template>
  <section class="about_book" ref="sectionRef" id="framework">
    <div class="about_book_wrapper">
      <!-- <h2 ref="titleRef">This book is not for everyone.</h2>

      <p ref="para1Ref">
        It is not meant for people looking for motivation or reassurance, nor
        for people who believe patience will solve their problems.
      </p>
      <p ref="para2Ref">
        It's for those who did everything they were supposed to do but still
        felt that something was off. For those who put in the effort without a
        problem.
      </p>
      <p ref="para3Ref">
        Discipline and hard work aren't rewarded as well anymore. Some people
        saw that the advice they were given didn't match the outcomes they see.
        They realized this early but lacked a model for it.
      </p>
      <strong ref="strongRef">
        The Pillars of Wisdom exist for people who noticed these things on their
        own.
      </strong> -->
      <h2 ref="titleRef">This book is not for everyone.</h2>

      <p ref="para1Ref">
        It is not for people looking for motivation or reassurance. And it is
        not for people who believe that patience will solve their problems.
      </p>
      <p ref="para2Ref">
        It is for those who did everything they were supposed to do but still
        felt that something was off. For those who can put in the effort without
        fail.
      </p>
      <p ref="para3Ref">
        This book is for those who see that the advice they were given doesn’t
        match the outcomes they see. The ones that realized that discipline and
        hard work aren't rewarded as well anymore. For those who saw it early
        but are lacking a model for it.
      </p>
      <strong ref="strongRef">
        The Pillars of Wisdom exist for people who noticed these things on their
        own.
      </strong>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, nextTick } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

const sectionRef = ref(null);
const titleRef = ref(null);
const para1Ref = ref(null);
const para2Ref = ref(null);
const para3Ref = ref(null);
const strongRef = ref(null);

onMounted(async () => {
  await nextTick();

  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: sectionRef.value,
      start: "top 80%",
      toggleActions: "play none none none",
    },
  });

  tl.from(titleRef.value, {
    opacity: 0,
    y: 50,
    duration: 0.6,
    ease: "power3.out",
  });

  tl.from(para1Ref.value, {
    opacity: 0,
    y: 20,
    duration: 0.4,
    ease: "power3.out",
  });
  tl.from(para2Ref.value, {
    opacity: 0,
    y: 20,
    duration: 0.4,
    ease: "power3.out",
  });
  tl.from(para3Ref.value, {
    opacity: 0,
    y: 20,
    duration: 0.4,
    ease: "power3.out",
  });

  tl.from(strongRef.value, {
    opacity: 0,
    y: 20,
    duration: 0.4,
    ease: "power3.out",
  });
});
</script>

<style lang="scss">
.about_book {
  width: 100%;
  height: fit-content;
  padding-block: 128px;
  background: #edf0f4;

  &_wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    width: clamp(280px, 80%, 1000px);
    background: white;
    border: 1px solid #371c47;
    border-radius: 40px;
    padding: 6%;
    height: auto;
    margin: 0 auto;
    gap: 32px;

    @media screen and (max-width: 768px) {
      gap: 25px;
    }
    @media screen and (max-width: 480px) {
      width: clamp(280px, 90%, 1000px);
      gap: 20px;
    }
    @media screen and (max-width: 375px) {
      width: clamp(280px, 95%, 1000px);
      gap: 15px;
    }
  }

  h2 {
    font-size: 2.5rem;
    font-weight: 700;
    font-family: "Libre Baskerville", sans-serif;
    font-style: normal;
    line-height: 150%;

    @media screen and (max-width: 768px) {
      font-size: 1.875rem;
      line-height: 130%;
    }

    @media screen and (max-width: 480px) {
      font-size: 1.6rem;
    }

    @media screen and (max-width: 375px) {
      font-size: 1.5rem;
    }
  }

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

    // @media screen and (max-width: 480px) {
    //   font-size: 1rem;
    // }

    // @media screen and (max-width: 375px) {
    //   font-size: 0.9rem;

    // }
  }

  strong {
    font-size: 1.25rem;
    font-weight: 700;
    font-family: 'Josefin Sans', sans-serif;
    font-style: normal;
    line-height: 150%;

    @media screen and (max-width: 768px) {
      font-size: 1.125rem;
      line-height: 130%;
    }

    @media screen and (max-width: 480px) {
      font-size: 1rem;
    }

    @media screen and (max-width: 375px) {
      font-size: 0.9rem;
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
