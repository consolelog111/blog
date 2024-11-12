<template>
  <div class="home" :style="{paddingBottom: aniHeight + 'px'}">
    <div class="initial">
      <div class="middle">
        <div>
          <span class="line" ref="main"></span>
        </div>
        <div class="name font-serif font-semibold">
          <div class="char">J</div>
          <div class="char">I</div>
          <div class="char">A</div>
          <div class="char">S</div>
          <div class="char">H</div>
          <div class="char">U</div>
          <div class="char text-[#d6ceaa]">.</div>
          <div class="char">L</div>
          <div class="char">I</div>
          <div class="char">U</div>
        </div>
        <span class="developer font-mono">A Full-Stack Developer🐱</span>
      </div>
      <div class="animation" id="animation"></div>
    </div>
    <div class="content" :style="{ marginTop: '-'+ aniHeight + 'px', minHeight: aniHeight + 'px'}"> 
      <div class="box mb-5">
        <span class="text1 font-mono text-4xl">Why Me?</span>
      </div>
      <div class="label flex mt-10 justify-around w-full"> 
        <div class="learn bg-white w-1/4 h-full pt-5 pb-10 px-10 rounded-lg shadow-xl flex flex-col items-center">
          <img src="../assets/uh_logo.png" class="w-1/3"/>
          <div class="font-mono font-semibold text-2xl mt-2 mb-3">&lt; Learning /></div>
          <div class="font-mono "> 
            <div class="font-semibold text-red-400">Master's programme: </div>
            <span>Computer Science (network track)</span>
          </div>
          <div class="font-mono mt-1"> 
            <div class="font-semibold text-red-400">Course topic: </div>
            <span>Network Protocols / Machine Learning / Data analysis / Big data platforms</span>
          </div>
        </div>
        <div class="experience bg-white w-1/4 h-full pt-5 pb-10 px-10 rounded-lg shadow-xl flex flex-col items-center">
          <img src="../assets/experience.png" class="w-1/3"/>
          <div class="font-mono font-semibold text-2xl mt-2 mb-3">&lt; Experience /></div>
          <div class="font-mono">
          <!-- Full-Stack Developer (Intern) at Eficode -->
          <div class="font-semibold text-red-400">May 2024 – Aug 2024</div>
          <span class="inline-block font-semibold">Full-Stack Developer- Eficode</span>
          <span class="inline-block">
            Developed and maintained web accessibility monitoring projects, implemented real-time audit status retrieval, automated Azure resource deployment, and ensured WCAG 2 compliance.
          </span>
        </div>

        <div class="font-mono mt-2">
          <!-- Full-Stack Developer & Back-End Developer at Inspur -->
          <div class="font-semibold text-red-400">Aug 2022 – Jul 2019</div>
          <span class="inline-block font-semibold">Full-Stack & Back-End Developer - Inspur</span>
          <span class="inline-block">
            Contributed to developing high-concurrency systems, refactored backend architectures, modularized core functionalities, and integrated systems with a microservices platform.
          </span>
        </div>
        </div>
        <div class="skill bg-white w-1/4 h-full pt-5 pb-10 px-10 rounded-lg shadow-xl flex flex-col items-center">
          <img src="../assets/skill.png" class="w-1/3"/>
          <div class="font-mono font-semibold text-2xl mt-2 mb-3">&lt; Skills /></div>
          <div class="font-mono">
          <div class="font-semibold text-red-400">Back-End Stack</div>
            <span>Java, Python, Node.js, Spring, Docker, Kubernetes, Nginx</span>
          </div>

          <div class="font-mono mt-1">
            <div class="font-semibold text-red-400">Front-End Stack</div>
            <span>JavaScript, TypeScript, HTML5, CSS3, ES6, Vue.js, React, Next.js</span>
          </div>

          <div class="font-mono mt-1">
            <div class="font-semibold text-red-400">Cloud Platforms</div>
            <span>Familiar with cloud computing platforms. Certified as an Azure Developer Associate.</span>
          </div>

        </div>
      </div>
    </div>
    <div v-show="isOverlayVisible" class="overlay w-full h-full">
      <button class="float-right mt-5 mr-10" @click="closeMenu">
        <div class="close-icon"></div>
      </button>
      <div class="flex w-full h-full justify-between px-10">
        <div class="menu h-full flex flex-col justify-around text-white pb-20 font-mono w-3/4">
          <button class="menu1 text-7xl text-left hover:text-[#42b883]  transition-all duration-300" @click="toHome()"><span>.isHome() </span><span class="text-base">01</span></button>
          <button class="menu2 text-7xl text-left hover:text-[#5876e3] transition-all duration-300" @click="toHome()">.isBlog() <span class="text-base">02</span></button>
          <button class="menu3 text-7xl text-left hover:text-[#e36868] transition-all duration-300" @click="toHome()">.isProject() <span class="text-base">03</span></button>
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
            <span class="text-yellow-500/65 text-2xl underline decoration-2 underline-offset-2">Follow me?</span>
            <span class="text-white text-lg">Github(Loading....)</span>
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
      const t = gsap.timeline({});
      t.fromTo('.menu1', { y: 10, opacity: 0 }, { y: 0, opacity: 1,duration: 0.3})
      t.fromTo('.menu2', { y: 10, opacity: 0 }, { y: 0, opacity: 1,duration: 0.3 })
      t.fromTo('.menu3', { y: 10, opacity: 0 }, { y: 0, opacity: 1,duration: 0.3 })
    },
    closeMenu() {
      window.scrollTo({
        top: 0,
        behavior: 'smooth'
      });
      const t = gsap.timeline({});
      t.fromTo('.menu1', { y: 0, opacity: 1 }, { y: 20, opacity: 0,duration: 0.1})
      t.fromTo('.menu2', { y: 0, opacity: 1 }, { y: 20, opacity: 0,duration: 0.1 })
      t.fromTo('.menu3', { y: 0, opacity: 1 }, { y: 20, opacity: 0,duration: 0.1 })
      t.to('.overlay', {
        opacity: 0,
        ease: 'Expo.easeInOut',
        duration:1
      }).then(() => {
        this.isOverlayVisible = false
      })
    },
  },
  setup() {
    const c = ref();
    const main = ref();
    const aniHeight = ref(0);
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
        // onUpdate: self => {
        //   console.log("progress:", self.progress.toFixed(3), "direction:", self.direction, "velocity", self.getVelocity());
        // }
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

      const t1 = gsap.timeline({});
      const anim2 = t1.fromTo('.text1', {
        opacity: 0,
      },{
        opacity: 1,
        duration: 0.8
      });

      ScrollTrigger.create({
        trigger: '.text1',
        animation: anim2,
        // markers: true,
        start: "top bottom",
        end: "top top",
        toggleActions: 'play none none none',
      });

      t1.fromTo('.label', { y: 0, opacity: 0 }, { y: 10, opacity: 1,duration: 0.3})
      aniHeight.value = document.getElementById("animation").offsetHeight

    });

    return { c,main,aniHeight };
  } 
};
</script>



<style lang="scss" scoped>

.home {
  width: 100%;
  height: 100%;
  position: relative;
}

.initial{
  width: 100%;
  height: 100%;
  position: relative;
  overflow-x: hidden;
}


.middle{
  z-index: 11;
  margin-top: 25vh;
  margin-left: 4rem;
  display: flex;
  flex-direction: column;
  position: relative;
  .line {
    width: 100%;
    max-width: 50rem;
    height: 0.5rem;
    position: relative;
    display: inline-block;
    background-color:#a7dbd8;
    border-radius: 5px; 
  }
  .name {
    line-height: 10rem;
    font-size: 10rem;
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
    margin-top: 0.5rem;
    font-size: 30px;
    color: white;
  }
}

.animation{
  top:-50vh;
  left: 40vw;
  width: 125vh;
  height: 125vh;
  border: #fa6900 solid 10px;
  z-index: 10;
  rotate: 35deg;
}

.content{
  position: absolute;
  width: 100%; 
}


.box {
  text-align: center;
  width: 100%;
  color: #fff;
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