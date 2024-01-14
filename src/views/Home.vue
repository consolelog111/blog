<template>
  <div class="home">
    <div class="initial">
      <div class="top font-mono">
        <el-button class="left-name">&lt;Shuu/></el-button>
        <el-button class="right-botton" @click="openMenu"><span>.Click()</span><span>:void</span></el-button>
      </div>
      <div class="middle">
        <div>
          <span class="line" ref="main"></span>
        </div>
        <div class="name font-mono">
          <div class="char">J</div>
          <div class="char">I</div>
          <div class="char">A</div>
          <div class="char">S</div>
          <div class="char">H</div>
          <div class="char">U</div>
          <div class="char text-yellow-500">.</div>
          <div class="char">L</div>
          <div class="char">I</div>
          <div class="char">U</div>
        </div>
        <span class="developer font-mono">A Full-Stack Developer🐱</span>
      </div>
      <div class="animation"></div>
    </div>
    <div class="content"> 
      <div class="box">
        <span class="text1">WHY ME?</span>
      </div>

      <div class="heart-button" @click="init">
          <div class="heart-box">
            <!-- Hearts will be appended here -->
          </div>
        </div>
    </div>

    <div class="text-600">
      <h2 class="">Thanks for Watching :)</h2>
    </div>
    
    <div v-show="isOverlayVisible" class="overlay w-full h-full">
      <button class="float-right mt-5 mr-10" @click="closeMenu">
        <div class="close-icon"></div>
      </button>
      <div class="flex w-full h-full justify-between px-10">
        <div class="menu h-full flex flex-col justify-around text-white pb-20 font-mono w-3/4">
          <button class="text-7xl text-left hover:text-[#42b883]  transition-all duration-300" @click="toHome()"><span>.isHome() </span><span class="text-base">01</span></button>
          <button class="text-7xl text-left hover:text-[#5876e3] transition-all duration-300" @click="toHome()">.isBlog() <span class="text-base">02</span></button>
          <button class="text-7xl text-left hover:text-[#e36868] transition-all duration-300" @click="toHome()">.isCategory() <span class="text-base">03</span></button>
        </div>
        <div class="info flex h-full flex-col justify-center font-mono w-1/4">
          <div class="info-item flex flex-col mb-5"> 
            <span class="text-yellow-500/65 text-2xl underline decoration-2 underline-offset-2">Where am I?</span>
            <span class="text-white text-lg">Helsinki</span>
          </div>
          <div class="info-item flex flex-col mb-5"> 
            <span class="text-yellow-500/65 text-2xl underline decoration-2 underline-offset-2">How to contact me?</span>
            <span class="text-white text-lg">jiashuliu.js@gmail.com</span>
            <span class="text-white text-lg">+358 0415765749</span>
          </div>
          <div class="info-item flex flex-col"> 
            <span class="text-yellow-500/65 text-2xl underline decoration-2 underline-offset-2">Follow me</span>
            <span class="text-white text-lg">Git</span>
          </div>
        </div>
    </div>
    </div>

    <el-backtop :right="30" :bottom="100">
      <div
      style="
        height: 100%;
        width: 100%;
        font-size: 46px;
        background-color: var(--el-bg-color-overlay);
        box-shadow: var(--el-box-shadow-lighter);
      "
    >
      👆
      </div>
    </el-backtop>
</div>
</template>


<script>
import { onMounted, onUnmounted, ref } from "vue";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

export default {

  data() {
    return {
      isOverlayVisible: false,
    };
  },
  methods: {
    toHome() {
      this.$router.push({ path: "/" });
    },
    openMenu() {
      this.isOverlayVisible = true;
      gsap.fromTo('.overlay', {opacity: 0}, {
        opacity: 1,
        ease: 'Expo.easeInOut',
        duration:0.8
      })
    },
    closeMenu() {
      window.scrollTo({
        top: 0,
        behavior: 'smooth'
      });
      gsap.to('.overlay', {
        opacity: 0,
        ease: 'Expo.easeInOut',
        duration:0.6
      }).then(() => {
        this.isOverlayVisible = false
      })
    },
    init() {
      const directions = ['up', 'leftup', 'rightup'];
      const direction = directions[Math.floor(Math.random() * directions.length)];

      const button = this.$el;
      const top = button.offsetTop;
      const left = button.offsetLeft;

      const newHeart = document.createElement('div');
      newHeart.className = `heart animate-${direction}`;

      const heartBox = button.querySelector('.heart-box');
      heartBox.style.top = `${top}px`;
      heartBox.style.left = `${left}px`;
      heartBox.style.zIndex = `999`;

      heartBox.appendChild(newHeart);
      console.log(heartBox);

      setTimeout(() => this.removeFirst(), 5000);
    },
    removeFirst() {
      const heartBox = this.$el.querySelector('.heart-box');
      const firstHeart = heartBox.querySelector('.heart:first-child');

      if (firstHeart) {
        firstHeart.remove();
      }
    },
  },
  setup() {

    
    const c = ref();
    const main = ref();
    gsap.registerPlugin(ScrollTrigger);

    onMounted(() => {
      // line
      gsap.from(main.value, {
        scaleX: 0, 
        duration: 2, 
        transformOrigin: "left center", 
        ease: "none"
      });

      // Or you can attach a tween or timeline to a ScrollTrigger later
      const anim = gsap.to('.animation', {
        rotation: 200,
        scale: 0.5, // 缩小为原来的一半
        opacity: 0, // 完全透明
        duration: 1, // 动画持续时间
        ease: "power2.inOut" // 缓动函数，可以根据需要调整
      });

      const trigger = ScrollTrigger.create({
        trigger: '.animation',
        animation: anim,
        // markers: true,
        start: "top center",
        end: "top+=100px top",
        toggleClass: "active",
        pin: true,
        scrub: 1,
        onUpdate: self => {
          console.log("progress:", self.progress.toFixed(3), "direction:", self.direction, "velocity", self.getVelocity());
        }
      });

      const t = gsap.timeline({});
        t.to(".char", {
          opacity: 1,
          delay: .1,
          duration: .2,
          y: 0,
          ease: "Power4.inOut",
          stagger: 0.1,
        })

        t.fromTo('.developer', { y: '-30px', opacity: 0 }, { y: 0, opacity: 1 })

      t.add(anim);
      t.add(() => {}, "+=0.01"); // 空的回调，用于确保 ScrollTrigger 在第一帧时就触发
      t.add(trigger.update);

      // // 启用 ScrollTrigger
      ScrollTrigger.refresh();

    
      t.from('.text1', {x:innerWidth * 1})

        
    });

    onUnmounted(() => {
      // ctx.value.revert(); // <- Easy Cleanup!
    });

    return { c,main };
  } 
};
</script>



<style lang="scss" scoped>

.home {
  width: 100%;
  height: auto;
  background-color: #fff;
}

.initial{
  background-color: #18181b;
  width:100%;
  position: relative;
  overflow-x: hidden;
}

.top{
  padding: 15px 0;
  display: flex;
  justify-content: space-between;
  height: 50px;
  width: 100%;
  color: #fff;
  position: relative;
  z-index: 9;
  .left-name{
    margin-left: 20px;
    font-size: 34px;
    font-weight: 600;
  }
  .right-botton{
    margin-right: 50px;
    text-decoration: none; 
    transition: text-decoration 0.1s ease; 
    line-height: 30px;
    span:nth-child(1){
      color: grey;
      font-size: 28px;
      font-weight: 400;
    }
    span:nth-child(1):hover{
      color: white;
    }
    span:nth-child(2){
      color: yellow;
      font-size: 26px;
      font-weight: 400;
    }
  }
  .right-botton:hover {
    text-decoration: underline;
    text-decoration-color: orange; 
    text-decoration-thickness: 3px; 
    text-underline-offset: 8px;
  }


  .right-botton:before {
    content: "";
    position: fixed;
    background: #09090b;
    bottom: 0;
    left: 0;
    right: 0;
    top: 100%;
    z-index: -1;
    transition: top 0.65s ease-out;
  }

  .right-botton:hover:before {
    top: 0;
  }
}

.middle{
  z-index: 11;
  margin-top:20vh;
  margin-left: 50px;
  display: flex;
  flex-direction: column;
  position: relative;
  .line {
    width: 100%;
    max-width: 660px;
    height: 8px;
    position: relative;
    display: inline-block;
    background-color:lightskyblue;
    border-radius: 5px; 
  }
  .name {
    line-height: 8rem;
    font-size: 7rem;
    position: relative;
    color: white;
    clip-path: polygon(0 0, 100% 0, 100% 100%, 0% 100%);
  }

  .char {
    font-size: 7rem;
    display: inline-block;
    margin-right: 6px;
    opacity: 0.3;
    transform: translateY(-150px);
    transition: transform .3s ease-in-out;
  }
  .developer{
    margin-top: 5px;
    font-size: 30px;
    color: white;
  }
}

.animation{
  top:-50vh;
  left: 40vw;
  width: 125vh;
  height: 125vh;
  border: orange solid 10px;
  z-index: 10;
  rotate: 35deg;
}

.content{
  position: absolute;
  width: 100%; 
  height: 10vh;
  margin-top:-150vh;
  // background-color:burlywood;
}


.box,
.box2 {
  text-align: center;
  position: relative;
  width: 90%;
  color: #fff;
  min-height: 100vh;
  font-size: 32px;
}

.box2 {
  h2 {
    font-size: 3em;
  }
}

.overlay {
  background-color: rgba(32, 36, 80);
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 999
}

.overlay::before {
  content: "isMenu()";
  font-size: 20rem;
  text-align: center;
  position: absolute;
  font-family: ui-serif, Georgia, Cambria, "Times New Roman", Times, serif;
  top: calc(50% - 15rem);
  left: 0;
  width: 100%;
  height: 100%;
  color: #f2f2f2; 
  opacity: 0.05; 
  z-index: -1; 
}


.close-icon {
  position: relative;
  width: 35px;
  height: 35px;
}

.close-icon::before,
.close-icon::after {
  content: "";
  position: absolute;
  width: 100%;
  height: 2px;
  background-color: #fff;
  top: 50%;
  left: 0;
  transform: translateY(-50%);
}

.close-icon::before {
  transform: rotate(45deg);
}

.close-icon::after {
  transform: rotate(-45deg);
}

.heart-icon {
  background-image: url("data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz48c3ZnIHdpZHRoPSIyMHB4IiBoZWlnaHQ9IjE4cHgiIHZpZXdCb3g9IjAgMCAyMCAxOCIgdmVyc2lvbj0iMS4xIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIj4gICAgICAgIDx0aXRsZT5oZWFydDwvdGl0bGU+ICAgIDxkZXNjPkNyZWF0ZWQgd2l0aCBTa2V0Y2guPC9kZXNjPiAgICA8ZGVmcz48L2RlZnM+ICAgIDxnIGlkPSJQYWdlLTEiIHN0cm9rZT0ibm9uZSIgc3Ryb2tlLXdpZHRoPSIxIiBmaWxsPSJub25lIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiPiAgICAgICAgPGcgaWQ9ImhlYXJ0IiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtNi4wMDAwMDAsIC03LjAwMDAwMCkiIGZpbGw9IiNEMDAyMUIiPiAgICAgICAgICAgIDxwYXRoIGQ9Ik0xNS41MjM4MDk1LDI1IEMxNiwyNSAxNiwyNSAxNi40NzYxOTA1LDI1IEwyNC4wOTUyMzgxLDE3IEMyNi41NDk4Njc5LDE0LjUxMzUwNDIgMjYuNTQ5ODY3OSwxMC45MDAxNDM2IDI0LjA5NTIzODEsOSBDMjIuMTUwOTIzNSw2LjQ0MjgzNjc3IDE4LjU4NDg3NSw2LjQ0MjgzNjc3IDE2LjQ3NjE5MDUsOSBDMTYsOSAxNiw5IDE1LjUyMzgwOTUsOSBDMTMuNDE1MTI1LDYuNDQyODM2NzcgOS44NDkwNzY0Niw2LjQ0MjgzNjc3IDcuOTA0NzYxOSw5IEM1LjQ1MDEzMjA3LDEwLjkwMDE0MzYgNS40NTAxMzIwNywxNC41MTM1MDQyIDcuOTA0NzYxOSwxNyBMMTUuNTIzODA5NSwyNSBaIj48L3BhdGg+ICAgICAgICA8L2c+ICAgIDwvZz48L3N2Zz4=");
  background-repeat: no-repeat;
  height: 22px;
  width: 22px;
}

.heart {
  ::v-deep {
    @extend .heart-icon;
    position: absolute;
  }
}

@mixin animation($move, $duration, $sideduration) {
  -webkit-animation: $move $duration 0s linear infinite, sideWays $sideduration 0s ease-in-out infinite alternate;
  -moz-animation: $move $duration 0s linear infinite, sideWays $sideduration 0s ease-in-out infinite alternate;
  -o-animation: $move $duration 0s linear infinite, sideWays $sideduration 0s ease-in-out infinite alternate;
  -ms-animation: $move $duration 0s linear infinite, sideWays $sideduration 0s ease-in-out infinite alternate;
  animation: $move $duration 0s linear infinite, sideWays $sideduration 0s ease-in-out infinite alternate;
}

.animate-up {
  z-index: inherit;
  ::v-deep {
    position: absolute;
    @include animation(moveUp, 5s, 2s);
  }
}

.animate-leftup {
  ::v-deep {
    position: absolute;
    @include animation(moveLeftUp, 5s, 2s);
  }
}

.animate-rightup {
  ::v-deep {
    position: absolute;
    @include animation(moveRightUp, 5s, 2s);
  }
}

@keyframes moveUp {
  0% {
    bottom: 0;
    transform: scale(0);
    opacity: 0;
  } 
  1% {
    bottom: 50%;
    transform: scale(.9);
    opacity: 1;
  } 
  50% {    
    opacity: 1;
  }  
  100% {
    bottom: 1000%;
    transform: scale(.5);
    opacity: 0;
  }
}

@keyframes moveLeftUp {
  0% {
    left: 0;
    bottom: 0;
    transform: scale(0);
    opacity: 0;
  } 
  1% {
    bottom: 50%;
    transform: scale(.9);
    opacity: 1;
  } 
  50% {
    left: -250%;
    opacity: 1;
  }  
  100% {
    left: -500%;
    bottom: 1000%;
    transform: scale(.5);
    opacity: 0;
  }
}

@keyframes moveRightUp {
  0% {
    left: 0;
    bottom: 0;
    transform: scale(0);
    opacity: 0;
  } 
  1% {
    bottom: 50%;
    transform: scale(.9);
    opacity: 1;
  } 
  50% {
    left: 250%;
    opacity: 1;
  }  
  100% {
    left: 500%;
    bottom: 1000%;
    transform: scale(.5);
    opacity: 0;
  }
}

@keyframes sideWays {
  0% {
    margin-left: 0px;
  }
   100% {
    margin-left: 30px;
  }
}

.content {
  padding: 200px;
}

.heart-button {
  position: relative;
  ::v-deep {
    @extend .heart-icon;
    display: inline-block;
    cursor: pointer;
  }
}
</style>