<template>
  <div class="home">
    <div class="initial">
      <div class="top font-mono">
        <el-button class="name-btn">&lt;Shuu/></el-button>
        <button class="menu-btn" @click="openMenu">
          <span>.Click()</span><span>:void</span>
        </button>
      </div>
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
            <div class="font-semibold text-red-400">01.2022 - 05.2023</div>
            <span class="inline-block font-semibold">Full-Stack Developer</span>
            <span class="inline-block">Participate in frontend project design, framework selection, overcoming technical challenges, and implementing feature development. Proficiently utilize mainstream JavaScript libraries and development frameworks.</span>
          </div>
          <div class="font-mono mt-2"> 
            <div class="font-semibold text-red-400">07.2019 - 12.2021</div>
            <span class="inline-block font-semibold">Back-end Developer</span>
            <span class="inline-block">Responsible for core module development, feature iteration, daily monitoring, troubleshooting, data backup, performance bottleneck analysis, and other related tasks in project management.</span>
          </div>
        </div>
        <div class="skill bg-white w-1/4 h-full pt-5 pb-10 px-10 rounded-lg shadow-xl flex flex-col items-center">
          <img src="../assets/skill.png" class="w-1/3"/>
          <div class="font-mono font-semibold text-2xl mt-2 mb-3">&lt; Skills /></div>
          <div class="font-mono "> 
            <div class="font-semibold text-red-400">Back-end</div>
            <span>Java, SQL, Linux, Docker, Dubbo, ZooKeeper</span>
          </div>
          <div class="font-mono mt-1"> 
            <div class="font-semibold text-red-400">Front-end</div>
            <span>JavaScript, TypeScript, HTML5, CSS3, Vue.js, React.js, Next.js, Tailwind</span>
          </div>
          <div class="font-mono mt-1"> 
            <div class="font-semibold text-red-400">Data Engineering</div>
            <span>MySQL, Oracle, MongoDB, Kafka, RabbitMQ, Redis</span>
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
    });

    return { c,main };
  } 
};
</script>



<style lang="scss" scoped>

.home {
  width: 100%;
  height: 100%;
  padding-bottom: 50px;
  background-color: #18181b;
  background: -moz-radial-gradient(0% 100%, ellipse cover, rgba(104,128,138,.4) 10%,rgba(138,114,76,0) 40%),-moz-linear-gradient(top, rgba(57,173,219,.25) 0%, rgba(42,60,87,.4) 100%), -moz-linear-gradient(-45deg, #670d10 0%, #092756 100%);
  background: -webkit-radial-gradient(0% 100%, ellipse cover, rgba(104,128,138,.4) 10%,rgba(138,114,76,0) 40%), -webkit-linear-gradient(top, rgba(57,173,219,.25) 0%,rgba(42,60,87,.4) 100%), -webkit-linear-gradient(-45deg, #670d10 0%,#092756 100%);
  background: -o-radial-gradient(0% 100%, ellipse cover, rgba(104,128,138,.4) 10%,rgba(138,114,76,0) 40%), -o-linear-gradient(top, rgba(57,173,219,.25) 0%,rgba(42,60,87,.4) 100%), -o-linear-gradient(-45deg, #670d10 0%,#092756 100%);
  background: -ms-radial-gradient(0% 100%, ellipse cover, rgba(104,128,138,.4) 10%,rgba(138,114,76,0) 40%), -ms-linear-gradient(top, rgba(57,173,219,.25) 0%,rgba(42,60,87,.4) 100%), -ms-linear-gradient(-45deg, #670d10 0%,#092756 100%);
  background: -webkit-radial-gradient(0% 100%, ellipse cover, rgba(104,128,138,.4) 10%,rgba(138,114,76,0) 40%), linear-gradient(to bottom, rgba(57,173,219,.25) 0%,rgba(42,60,87,.4) 100%), linear-gradient(135deg, #670d10 0%,#092756 100%);
}

.initial{
  width:100%;
  height: 100%;
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
  .name-btn{
    margin-left: 20px;
    font-size: 34px;
    font-weight: 600;
  }
  .menu-btn{
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
  .menu-btn:hover {
    text-decoration: underline;
    text-decoration-color: orange; 
    text-decoration-thickness: 3px; 
    text-underline-offset: 8px;
  }


  .menu-btn:before {
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

  .menu-btn:hover:before {
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
    max-width: 50rem;
    height: 8px;
    position: relative;
    display: inline-block;
    background-color:lightskyblue;
    border-radius: 5px; 
  }
  .name {
    line-height: 8rem;
    font-size: 8rem;
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
  height: 152vh;
  margin-top:-152vh;
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