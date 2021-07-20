<template>
<div class="h-screen fixed top-0 left-0  overflow-clip w-screen bg-gray-900">

  <div :style="`--tw-translate-y: ${-55-45*pinkBubble}%;--tw-translate-x: ${-40-60*pinkBubble}%;`" class="pink-bubble">

    <div class="fixed " style="bottom:37%;right:15%">
      <h1 class="text-8xl text-white font-bold tracking-wide">Hi! I'm Saumya!</h1>
    </div>
  </div>
  <div :style="`--tw-translate-x: ${20+48*greenBubble}%;--tw-translate-y:${-40-40*greenBubble}%;`" class=" green-bubble">
  </div>
  <div :style="`--tw-translate-x: -${22+78*blueBubble}%;--tw-translate-y:-${63+37*blueBubble}%;`" class="blue-bubble">
  </div>

  <div class="indicator hidden">{{Math.round(scroll)}}</div>
</div>
</template>

<script >
const html = document.documentElement;
const frameLength = 30;
const stall = 6;
export default {
  data:()=>({
    scroll: 0
  }),
  computed:{
    pinkBubble(){
      if (this.scroll <stall) return 0;
      if (this.scroll > frameLength) return 1;
      return (this.scroll-stall)/(frameLength-stall)
    },
    greenBubble(){
      if (this.scroll <(frameLength+stall)) return 0;
      if (this.scroll > (frameLength*2)) return 1;
      return (this.scroll-(frameLength+stall))/(frameLength-stall)
    },
    blueBubble(){
      if (this.scroll <(frameLength*2+stall*4)) return 0;
      if (this.scroll > (frameLength*4)) return 1;
      return (this.scroll-(frameLength*2+stall*4))/(frameLength*2-stall*4)
    }
  },
  mounted(){
    const scrollTop = html.scrollTop;
    const maxScrollTop = html.scrollHeight - window.innerHeight;
    this.scroll = Math.round(360 * scrollTop / maxScrollTop);
    window.addEventListener('scroll', event => {
      const scrollTop = html.scrollTop;
      const maxScrollTop = html.scrollHeight - window.innerHeight;
      this.scroll = 360 * scrollTop / maxScrollTop;
    });
  }
}

// This starter template is using Vue 3 experimental <script setup> SFCs
// Check out https://github.com/vuejs/rfcs/blob/master/active-rfcs/0040-script-setup.md
</script>

<style>
body {
  height: 1500vh;
  overscroll-behavior: none;
  overflow-x: hidden;
  overflow-y: scroll;

}
html {
  height: 100vh;
}
.indicator {
  z-index: 100;
  @apply  text-9xl font-bold text-white absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2;
}

.pink-bubble {
  height: 210vh;
  width:210vh;

  @apply rounded-full absolute transform z-50 bg-pink-700;

}

.green-bubble {
  width: 140vh;height:140vh;
  @apply z-40 absolute rounded-full transform  bg-green-400 right-0 top-0;
}

.blue-bubble {
  width: 300vh;height:300vh;
  @apply z-30 absolute rounded-full transform bg-blue-400  top-0;
}

::-webkit-scrollbar {
  width: 0;  /* Remove scrollbar space */
  background: transparent;  /* Optional: just make scrollbar invisible */
}
</style>
