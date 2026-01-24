<template>
  <section ref="section" class="parallax">
    <div ref="bg" class="parallax__bg"></div>
    <div class="parallax_text">
      <p>
        People who read this aren't looking for permission. They prefer a clear
        vision over optimism.
      </p>

      <p>
        People find this book when they've become tired of platitudes,
        shortcuts, and advice that doesn't lead anywhere.
      </p>
    </div>
  </section>
</template>


<!-- <script setup>
import { ref, onMounted, onUnmounted } from "vue";

const sectionRef = ref(null);
let ticking = false;

const handleScroll = () => {
  if (!sectionRef.value || ticking) return;

  ticking = true;

  requestAnimationFrame(() => {
    const rect = sectionRef.value.getBoundingClientRect();
    const offset = rect.top * 0.2;

    sectionRef.value.style.setProperty(
      "--parallax-offset",
      `${offset}px`
    );

    ticking = false;
  });
};

onMounted(() => {
  handleScroll();
  window.addEventListener("scroll", handleScroll);
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script> -->


<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const section = ref(null);
const bg = ref(null);

let ticking = false;

const handleScroll = () => {
  if (!section.value || !bg.value || ticking) return;

  ticking = true;

  requestAnimationFrame(() => {
    const rect = section.value.getBoundingClientRect();
    const vh = window.innerHeight;

    // прогресс нахождения секции во viewport
    const progress = Math.min(
      1,
      Math.max(0, (vh - rect.top) / (vh + rect.height))
    );

    // максимальный сдвиг фона
    const maxTranslate = bg.value.offsetHeight - section.value.offsetHeight;

    bg.value.style.transform = `translateY(${-maxTranslate * progress}px)`;

    ticking = false;
  });
};

onMounted(() => {
  handleScroll();
  window.addEventListener("scroll", handleScroll, { passive: true });
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<style lang="scss">


    .parallax {
        width: 100%;
        height: auto;
        position: relative;
        // background: #898989;
        color: white;
        padding-block: 192px;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;

        &__bg {
            // position: absolute;
            // inset: -50%;
            // background-image: url("@/public/images/parallax_bg.webp");
            // background-size: cover;
            // background-position: center;
            // background-repeat: no-repeat;
            // transform: translateY(var(--parallax-offset, 0));
            // will-change: transform;
            // z-index: 0;

            position: absolute;
            left: 0;
            top: 10%;
            width: 100%;
            height: 140%;
            transform: translateY(-50%);
            background-image: url("@/public/images/parallax_bg.webp");
            background-size: cover;
            background-position: center;
            will-change: transform;
            background-repeat: no-repeat;

        }

        &_text {
            display: flex;
            flex-direction: column;
            justify-content: flex-start;
            align-items: flex-start;
            max-width: 70%;
            gap: 40px;
        }
    }
</style>
