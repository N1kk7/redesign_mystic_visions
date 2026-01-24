<template>
    <section class="section promo-hero">
        <div 
            class="loader_component"
            v-if="loader"
        >
            <SharedLoader/>
        </div>
        <div class="container">
            <div class="promo-hero-content">
            <div class="left_column">
                <div class="text_content">
                <span>
                    Ready to get paid what you're worth, live where you're treated best,
                    and <span class="bold_text">start living your best life?</span></span>
                <h1>
                    Get INSTANT Access!
                </h1>
                <p>
                    <span class="bold_text">The Pillars of Wisdom is The #1 Playbook</span> for Hacking the Job Market,
                    Building Remote Freedom, and Winning at Life
                </p>
                </div>
                <div class="media_content">
                <video
                    v-if="isMobile"
                    ref="mobileVideo"
                    id="promo-video-mobile"
                    class="video-js vjs-default-skin w-full h-[60vh] min-h-[60vh] overflow-hidden"
                    playsinline
                    autoplay
                    muted
                    preload="auto"
                    poster="../public/images/preview1.webp"
                >
                    <!-- <source 
                        src="../public/videos/hero-final-cropped1.mp4" 
                        type="video/mp4" 
                    /> -->
                     <source 
                        src="https://pub-0a8d6c93bd2743669515202d259de491.r2.dev/hero-final-cropped1.mp4" 
                        type="video/mp4" 
                    />
                    Your browser does not support the video tag.
                </video>

                <video
                    v-else
                    ref="desktopVideo"
                    id="promo-video-desktop"
                    class="video-js vjs-default-skin w-full min-h-[60vh] h-[60vh] overflow-hidden"
                    playsinline
                    autoplay
                    muted
                    preload="auto"
                    poster="../public/images/video-desktop-preview.webp"
                >
                    <!-- <source 
                        src="../public/videos/Video-desktop-cropped.mp4" 
                        type="video/mp4" 
                    /> -->
                    <source 
                        src="https://pub-0a8d6c93bd2743669515202d259de491.r2.dev/Video-desktop-cropped.mp4" 
                        type="video/mp4" 
                    />
                    Your browser does not support the video tag.
                </video>
                <button 
                    v-if="!soundHidden"
                    class="sound_on_btn"
                    @click="unmuteVideo"
                >
                    <div class="warning">
                    <svg>
                        <use xlink:href="#no-sound-icon"></use>
                    </svg>
                    <span class="call-to-action">
                        click to turn
                        <br />
                        <span class="capitalize_text"> on sound </span>
                    </span>
                    </div>
                    <div class="sound_on">
                    <svg class="icon">
                        <use xlink:href="#volume-icon"></use>
                    </svg>
                    <span class="text"> Enable sound </span>
                    </div>
                </button>
                </div>
            </div>
            <div class="right_column">
                
                <NuxtImg
                    src="/images/promo-book-1200.webp"
                    sizes="(max-width: 480px) 480px, (max-width: 768px) 768px, 1200px"
                    alt="book"
                    style="width: 70%; height: auto;"
                />

                   
                <div class="bottom_content">
                <div class="rate_wrapper">
                    <div class="stars_content">
                    <svg class="icon">
                        <use xlink:href="#rate-star-icon"></use>
                    </svg>
                    <svg class="icon">
                        <use xlink:href="#rate-star-icon"></use>
                    </svg>
                    <svg class="icon">
                        <use xlink:href="#rate-star-icon"></use>
                    </svg>
                    <svg class="icon">
                        <use xlink:href="#rate-star-icon"></use>
                    </svg>
                    <svg class="icon">
                        <use xlink:href="#rate-star-icon"></use>
                    </svg>
                    </div>
                    <div class="rate_comment">5-Star Rating on <span class="bold_text">Goodreads</span></div>
                </div>
                <button
                    class="hero_btn"
                    @click="discountHandler"
                >
                <!-- modalStore.showModal('BookPromoModal') -->
                    <h2>Get Your Copy Now</h2>
                    <span> Exclusive Offer Awaits </span>
                </button>
                </div>
            </div>
            </div>
            <div class="promo_testimonials">
                <div class="testimonial-card">
                <img src="../public/images/pauli1.webp" alt="avatar" />
                <div class="slide_text">
                    <p>
                    The Pillars of Wisdom dives deeply into the psychological workings
                    of the conformists, individuals for whom “truth is so painful or
                    traumatic that it must always be denied — regardless of the
                    counterevidence.” There is no way to stop the stampede. The
                    important thing is to stay out of the frenzied herd’s way, wait
                    for it to deplete all its resources, and collapse from exhaustion.
                    </p>
                    <span class="author"> Dr. Pauli Brattico </span>
                </div>
                </div>
                <div class="testimonial-card">
                <img src="../public/images/antony1.webp" alt="avatar" />

                <div class="slide_text">
                    <p>
                    The Pillars of Wisdom is the Manosphere’s ultimate red pill bible
                    and the best book to ever come out of this god forsaken community.
                    </p>
                    <span class="author"> Anthony "Dream" Johnson </span>
                </div>
                </div>
        
            </div>
        </div>
    </section>



</template>



<script setup >

import { nextTick } from 'vue'
import videojs from "video.js";
import { ref, onMounted, onBeforeUnmount } from 'vue'
import 'video.js/dist/video-js.css'

const videoEl = ref(null);
const mobileVideo = ref(null);
const desktopVideo = ref(null);
const jsPlayer = ref(null);
const isPlaying = ref(true);
const soundHidden = ref(false);
const isMobile = ref(false);

const loader = ref(false);

const modalStore = useModalStore();

onMounted(async () => {

const width = window.screen.width;
  isMobile.value = width <= 650;

  await nextTick();

   const videoRef = isMobile.value ? mobileVideo.value : desktopVideo.value;

   if (!videoRef) {
    console.error('Video element not found!');
    return;
  };

  jsPlayer.value = videojs(videoRef, {
    autoplay: true,
    playsinline: true,
    muted: true,
    controls: true,
  })

//   jsPlayer.value = videojs(videoEl.value, {
//     autoplay: true,
//     playsinline: true,
//     muted: true,
//     controls: true,
//   })

  jsPlayer.value.on('ended', () => {
    isPlaying.value = false
  })

//   window.addEventListener('resize', () => {

//     const innerWidth = window.innerWidth
//     // console.log(innerWidth, "innerWidth");

//     innerWidth <= 650 ? isMobile.value = true : isMobile.value = false
//   })


})

const discountHandler = async () => {

    // TEMPORARY DISABLED

    // loader.value = true;
    // document.body.style.overflow = "hidden";


    // try{

    // const getLocation = await $fetch("/api/shared", {
    //     method: "GET",
    //     params: {
    //         method: "get-location",
    //     },
    // });


    // if (getLocation.data.country_code === "US") {

    //     setTimeout(() => {
    //         document.body.style.overflow = "unset";
    //         modalStore.showModal('BookPromoModal');
    //         loader.value = false
    //     }, 1200);

    // } else {

    //     setTimeout(() => {
    //         window.location.href = "https://shop.thepillarsofwisdom.com/cart/49305684803752:1";
    //         document.body.style.overflow = "unset";
    //         loader.value = false
    //     }, 1200);
        
    // }

    // } catch (err) {

    //     console.log(err, 'something went wrong')
    // }

    window.location.href = "https://shop.thepillarsofwisdom.com/cart/49305684803752:1";

}

onBeforeUnmount(() => {
  if (jsPlayer.value) {
    jsPlayer.value.dispose()
  }

//   window.removeEventListener('resize', () => {})
})

const unmuteVideo = () => {
  if (!jsPlayer.value) return
  soundHidden.value = true
  jsPlayer.value.muted(false)
  jsPlayer.value.currentTime(0)
  jsPlayer.value.play()
  isPlaying.value = true
}

const togglePlay = () => {
  const player = jsPlayer.value
  if (!player) return

  if (player.paused()) {
    player.play()
    isPlaying.value = true
  } else {
    player.pause()
    isPlaying.value = false
  }
}


</script>




<style lang="scss" scoped>

:deep(.vjs-big-play-button) {
  display: none !important;
}

#promo-video,
#promo-video-mobile {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.loader_component{
    background: rgba(255,255,255, 0.85);
    backdrop-filter: blur(3px);
    width: 100vw;
    height: 100vh;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 50;
}

.promo-hero{
    padding-top: 0 !important;
    .container{
        width: 80vw;
        @media screen and (max-width: 1024px) {
            width: 95vw;
        }
    }
    
    .promo-hero-content{
        display: grid;
        grid-template-columns: 2fr 1fr;
        width: 100%;
        height: auto;
        min-height: 100vh;
        padding-top: 20px;
        padding-bottom: 50px;
        overflow: hidden;
        gap: 20px;
        @media screen and (max-width: 768px) {
            &{
                display: flex;
                flex-direction: column;
                align-items: center;
                justify-content: flex-start;
                max-height: unset;
                height: auto;
            }
        
        }
    }
   
}
.left_column{
    display: flex;
    align-items: stretch;
    justify-content: flex-end;
    flex-direction: column;
    text-align: center;

    .text_content{
        height: -webkit-fill-available;
        width: 100%;
        margin: 0 auto;
        gap: 10px;
        color: rgb(41, 48, 72);
        display: flex;
        flex-direction: column;
        justify-content: center;
        span{
            font-size: clamp(1.2rem, 1.8vw, 2.5rem);
            font-family: 'Roboto', sans-serif;
            font-weight: 400;
            line-height: normal;
            // font-family: 'Roboto-Regular', sans-serif;
        }
        h1{
            font-size: clamp(2.1rem, 4.8vw, 4.5rem);
            font-family: 'DM Serif Display', sans-serif;
            font-weight: 600;
            color: rgb(41, 48, 72);

        }
        p{
            font-family: 'Roboto', sans-serif;
            text-align: center;
            font-size: clamp(1.2rem, 1.8vw, 2.5rem);
            color: rgb(41, 48, 72);
            line-height: normal;


        }
        .bold_text{
            font-family: 'Roboto', sans-serif;
            font-weight: 600;
        }
        @media screen and (max-width: 768px) {
            &{
                height: auto;
            }
            
        }
    }

}
.media_content{
    position: relative;
    background: black;
    margin-top: 20px;

    video{
        margin: 0 auto;
        height: 100%;
        max-height: 60vh;
        // object-fit: cover;
        object-fit: initial;
        width: 100%;
        // left: 50%;
        // transform: translateX(-50%);

        // @media screen and (max-width: 1024px) {
        //     width: 100%;
        // }

        @media screen and (max-width: 768px) {
            width: 100%;
        }

        @media screen and (max-width: 500px) {
            width: 90%;
        }
        @media screen and (max-width: 450px) {
            width: 100%;
        }
    }

    .call-to-action{
        white-space: nowrap;
    }

    .sound_on_btn{
        width: 100%;
        height: 90%;
        position: absolute;
        top: 0;
        left: 0;
        z-index: 10;
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        color: white;
    }
    .sound_on_hidden{
        display: none;
    }
    .warning{
        background: rgba(255, 255, 255, 0.1);
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 10px;
        margin: 10px;
        border-radius: 10px;
        text-transform: uppercase;
        font-weight: 600;
        gap: 10px;
        svg{
            background: red;
            width: 50px;
            height: 50px;
            padding: 8px;
            border-radius: 50%;
            @media screen and (max-width: 768px) {
                width: clamp(40px, 5vw, 50px);
                height: clamp(40px, 5vw, 50px);
            }
        }
        .capitalize_text{
            font-size: large;
        }
    }
    .sound_on{
        background: rgba(255, 255, 255, 0.1);
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 10px;
        margin: 10px;
        border-radius: 10px;
        text-transform: uppercase;
        font-weight: 600;
        gap: 10px;
        svg{
            background: green;
            padding: 8px;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            @media screen and (max-width: 768px) {
                width: clamp(40px, 5vw, 50px);
                height: clamp(40px, 5vw, 50px);
            }
        }
        @media screen and (max-width: 768px) {
            &{
                display: none;
            }
            
        }
        
    }
}
.right_column{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-end;
    margin-top: 45px;

    gap: 30px;
    @media screen and (max-width: 768px) {
        &{
            width: 100%;
        }
    }


}
.bottom_content{
    width: 100%;
}

.rate_wrapper{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: nowrap;
    width: 100%;
    gap: 20px;
    .rate_comment{
        font-family: 'Roboto', sans-serif;
        font-weight: 400;
        white-space: nowrap;
        font-size: auto;
        .bold_text{
        font-family: 'Roboto', sans-serif;
        font-weight: 600;

        }
    }
}
.stars_content{
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 7px;
    svg{
        width: 20px;
        height: 20px;
    }
}
.hero_btn{
    width: 100%;
    // background: #4b245e;
    background-color: rgb(0, 176, 10);
    padding: 20px 40px;
    white-space: nowrap;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border-radius: 10px;
    margin-top: 25px;
    border-top: none !important;
    border-left: none !important;
    border-right: none !important;
    border-bottom: 7px solid rgb(7 154 10);
    // border-color: #291334;
    border-width: 7px;
    gap: 2px;
    color: white ;

    h2{
        color: white;
        font-size: clamp(18px, 1.8vw, 32px);
        font-weight: 500;
    }
}
.promo_testimonials{
    width: 100%;
    height: auto;
    margin-top: 50px;
    display: flex;
    justify-content: center;
    align-items: stretch;
    gap: 30px;
    @media screen and (max-width: 768px) {
        flex-direction: column;
        margin-top: 0;
        
    }
    .testimonial-card{
        display: flex;
        justify-content: space-between;
        align-items: stretch;
        background: #fff;
        padding: 15px;
        height: auto;
        border-radius: 10px;
        gap: 15px;
        flex: 1;
        img{
            width: clamp(110px, 11vw, 220px);
            height: clamp(110px, 11vw, 220px);
            border-radius: 10px;
            @media screen and (max-width: 768px) {
                &{
                    width: 100%;
                    height: -webkit-fill-available;
                    padding-bottom: 15px;
                }
            }
        }
        .slide_text{
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;
            height: 100%;

            gap: 10px;
            p{
                font-family: 'Roboto', sans-serif;
                text-align: center;
                height: -webkit-fill-available;
                display: flex;
                align-items: center;
                justify-content: center;
                line-height: normal;
                font-size: 1.25rem;
                font-weight: 500;
                color: black;
                @media screen and (max-width: 768px) {
                    display: block;
                    height: auto;
                    
                }
            }
            span{
                font-family: 'DM Serif Display', sans-serif;
                // font-size: clamp(1.6rem, 1.8vw, 2.8rem);
                font-size: 1.6rem;
                font-weight: 700;
                text-align: center;
            }
        }
        @media screen and (max-width: 768px) {
            &{
                flex-direction: column;
                justify-content: flex-start;
            }
            
        }
    }
}


</style>