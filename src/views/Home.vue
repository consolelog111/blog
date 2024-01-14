<template>
  <div class="home">
    <div class="initial">
      <div class="top font-mono">
        <el-button class="left-name" @click="toHome()">&lt;Shuu/></el-button>
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
          <div class="char">.</div>
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
          <button class="text-7xl text-left" @click="toHome()">.isHome() <span class="text-base">01</span></button>
          <button class="text-7xl text-left" @click="toHome()">.isBlog() <span class="text-base">02</span></button>
          <button class="text-7xl text-left" @click="toHome()">.isCategory() <span class="text-base">03</span></button>
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
      isOverlayVisible: false
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
    }
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


      //   ScrollTrigger.create({
      //     trigger: ".box",
      //     start: "top 10%", //animation Start at this point
      //     markers: true,
      //     scrub: true,
      //     pin: true,
      //     onEnter: () => {
      //     gsap.from(".text1", { x: innerWidth * 1 })
      //   }
      // });
        
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
  background-color: #15151C;
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
    background: #000;
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
    color: white;
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

</style>