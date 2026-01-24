<template>
  <div class="header" :class="activeHeaderState ? 'active_header' : ''">
    <div class="container">
      <div class="header_content">
        <div :class="activeTitleState ? 'main_title_active':''" class="main_title">
          The Pillars of Wisdom
        </div>
        <NuxtLink 
          class="link_btn"
          to="https://shop.thepillarsofwisdom.com/checkouts/cn/hWN7tonVpbDOa9dDloNf0Veb/en-mx?_r=AQABpJ7nq5P6Qh6hehgo-XLUTSYHqH0Dn0u1owxTiPAR99A&auto_redirect=false&edge_redirect=true&skip_shop_pay=true"
          target="_blank"
        >
          Get the Book
        </NuxtLink>
        
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, watch } from "vue";

const activeHeaderState = ref(false);
const activeTitleState = ref(false);
const screenHeight = ref(0);

const handleScroll = () => {
    activeHeaderState.value = window.scrollY > 50
    activeHeaderState.value && (screenHeight.value >= window.scrollY) ? activeTitleState.value = true : activeTitleState.value = false
};





onMounted(() => {

  screenHeight.value = window.innerHeight;

    window.addEventListener('scroll', handleScroll);
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
})


</script>

<style scoped lang="scss">
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: fit-content;
  color: black;
  background-color: white;
  transition: all ease 0.3s;
  padding-block: 24px;

  font-weight: 300;
  z-index: 15;


  &_content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 10px;

    .main_title {
      font-family: "Merriweather", sans-serif;
      font-weight: 700;
      font-size: clamp(1.5rem, 3vw, 3rem);
      transition: all ease 0.4s;
      color: black;

      @media screen and (max-width: 480px) {
        font-size: clamp(1rem, 5vw, 1.5rem);
      }
    }

    .main_title_active {
      transition: all ease 0.4s;
      color: white;
}

    .link_btn {
      padding: 10px 30px;
      display: flex;
      justify-content: center;
      align-items: center;
      background: rgb(253, 130, 43);
      color: white;
      font-family: "Roboto", sans-serif;
      font-size: 1rem;
      font-weight: 500;
      border-radius: 30px;
      white-space: nowrap;
      transition: all ease 0.3s;

      @media screen and (min-width: 1024px) {
        &:hover {
          background: rgb(255, 112, 10);
        transition: all ease 0.3s;
        }
      }

      @media screen and (max-width: 480px) {
        padding: 10px 10px;
        font-size: 0.8rem;
      }
      @media screen and (max-width: 375px) {
        padding: 5px 5px;
        font-size: 0.7rem;
      }

      &:active {
        background: rgb(255, 112, 10);
        transition: all ease 0.3s;
      }
    }
  }

  @media screen and (max-width: 480px) {
    padding-block: 16px;
  }
  @media screen and (max-width: 375px) {
    padding-block: 12px;
  }





}

.active_header {
  backdrop-filter: blur(20px);
  transition: all ease 0.3s;
  background: rgba(255,255,255,0.25);
  padding-block: 16px;


}




</style>
