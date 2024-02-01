<template>
  <div>
    <div
      class="nav"
    >
      <div class="top font-mono">
          <el-button class="name-btn" color="#b9d7d9" @click="toHome()">&lt;Shuu/></el-button>
          <el-button class="menu-btn" @click="openMenu">
            <span>.Click()</span><span>:void</span>
          </el-button>
      </div>
    </div>
    <div v-show="isOverlayVisible" class="overlay w-full h-full">
      <button class="float-right mt-5 mr-10" @click="closeMenu">
        <div class="close-icon"></div>
      </button>
      <div class="flex w-full h-full justify-between px-10">
        <div class="menu h-full flex flex-col justify-around text-white pb-20 font-mono w-3/4">
          <button class="menu1 text-7xl text-left hover:text-[#42b883]  transition-all duration-300" @click="toHome()"><span>.isHome() </span><span class="text-base">01</span></button>
          <button class="menu2 text-7xl text-left hover:text-[#5876e3] transition-all duration-300" @click="toHello()">.isBlog() <span class="text-base">02 / Go live as soon as possible :D</span></button>
          <button class="menu3 text-7xl text-left hover:text-[#e36868] transition-all duration-300" @click="toHome()">.isProject() <span class="text-base">03 / This as well :D</span></button>
        </div>
        <div class="info flex h-full flex-col justify-center font-mono w-1/4">
          <div class="info-item flex flex-col mb-5"> 
            <span class="text-yellow-500/65 text-2xl underline decoration-2 underline-offset-2">Where am I?</span>
            <span class="text-white text-lg">Helsinki</span>
          </div>
          <div class="info-item flex flex-col mb-5"> 
            <span class="text-yellow-500/65 text-2xl underline decoration-2 underline-offset-2">How to contact me?</span>
            <span class="text-white text-lg">jiashuliu.js@gmail.com</span>
            <span class="text-white text-lg">+358 415765749</span>
          </div>
          <div class="info-item flex flex-col"> 
            <span class="text-yellow-500/65 text-2xl underline decoration-2 underline-offset-2">Follow me?</span>
            <span class="text-white text-lg">Github(Still Loading....)</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import {
  defineComponent,
  defineAsyncComponent,
  reactive,
} from "vue";
import service from "../utils/https";
import urls from "../utils/urls";
import { useStore } from "vuex";
import { useRoute, useRouter } from "vue-router";
import { ElLoading, ElMessage } from "element-plus";
import { key } from "../store";
import { isMobileOrPc, getQueryStringByName } from "../utils/utils";
import { UserInfo, NavListItem } from "../types/index";

export default defineComponent({
  name: "NavBar",
  computed: {

  },
  data() {
    return {
      isOverlayVisible: false
    };
  },
  methods: {
    toHome() {
      this.closeMenu()
      this.$router.push({ path: "/" });
    },
    toHello() {
      this.closeMenu()      
      // this.$router.push({ path: "/helloWorld" });
    },
    openMenu() {
      this.isOverlayVisible = true
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
  watch: {
    $route: {
      handler(val: any, oldVal: any) {
        this.routeChange(val, oldVal);
      },
      immediate: true,
    },
  },
  mounted() {
    // 授权登录的，有 code 参数
    this.routeChange(this.$route, this.$route);
  },
  setup(props, context) {
    const store = useStore(key);
    const router = useRouter();
    const state = reactive({
      visible: false,
      handleFlag: "",
      title: "首页",
      list: [
        {
          index: "1",
          path: "/",
          name: "首页",
        },
        {
          index: "2",
          path: "/articles",
          name: "文章",
        },
        {
          index: "3",
          path: "/archive",
          name: "归档",
        },
        {
          index: "4",
          path: "/project",
          name: "项目",
        },
        {
          index: "5",
          path: "/timeline",
          name: "历程",
        },
        {
          index: "6",
          path: "/message",
          name: "留言",
        },
        {
          index: "7",
          path: "/about",
          name: "关于",
        },
      ] as Array<NavListItem>,
      activeIndex: "0",
      enterSlideUp: false,
      leaveSlideDown: false,
      isShow: false,
      isMobile: isMobileOrPc(),
    });

    const routeChange = (val: any, oldVal: any) => {
      for (let i = 0; i < state.list.length; i++) {
        const l: NavListItem = state.list[i];
        if (l.path === val.path) {
          state.activeIndex = i + 1 + "";
          state.title = l.name;
          break;
        }
      }
    };

    const handleSelect = (val: string, oldVal: string): void => {
      state.activeIndex = val;
    };

    const handleOk = (value: boolean): void => {
      state.visible = value;
    };

    const handleCancel = (value: boolean): void => {
      state.visible = value;
    };

    const handleClick = (value: string): void => {
      state.handleFlag = value;
      state.visible = true;
    };

    const handleLogout = (): void => {
      window.sessionStorage.userInfo = "";
      store.commit("SAVE_USER", {
        userInfo: {
          _id: "",
          name: "",
          avatar: "",
        },
      });
    };

    const handleClickMenu = (route?: string): void => {
      state.isShow = false;
      if (route === "/login") {
        state.handleFlag = "login";
        state.visible = true;
      }
      if (route === "/register") {
        state.handleFlag = "register";
        state.visible = true;
      }
      if (route === "/logout") {
        handleLogout();
      }
    };

    const handleMenu = (): void => {
      state.isShow = true;
      state.enterSlideUp = true;
    };

    const handleHideMenu = (): void => {
      state.enterSlideUp = false;
      state.leaveSlideDown = true;
      setTimeout(() => {
        state.leaveSlideDown = false;
        state.isShow = false;
      }, 300);
    };

    return {
      state,
      handleCancel,
      handleOk,
      handleClick,
      handleLogout,
      handleClickMenu,
      handleMenu,
      handleSelect,
      routeChange,
      handleHideMenu
    };
  },
});
</script>

<style scoped lang="less">
.nav-mobile {
  display: flex;
  line-height: 60px;
  .nav-mobile-logo {
    flex: 1;
    margin-top: 5px;
    margin-left: 10px;
  }
  .title {
    flex: 3;
    font-size: 24px;
  }
  .menu {
    flex: 1;
    font-size: 34px;
    color: #409eff;
  }
}
.nav-mobile-content {
  font-size: 0.3rem;
  height: 7.3rem;
  width: 100%;
  background-color: #fff;
  .list {
    .item {
      line-height: 0.8rem;
      color: #303133;
      border-bottom: 1px solid #eee;
      a {
        display: block;
        width: 100%;
        color: #409eff;
        text-decoration-line: none;
      }
    }
  }
}
.nav {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1000;
  width: 100%;
  .nav-content {
    width: 1200px;
    margin: 0 auto;
  }
  .logo {
    height: 50px;
    margin: 0;
    border-radius: 50%;
    margin-top: 5px;
  }
  .el-menu.el-menu--horizontal {
    border-bottom: none;
  }
  .el-menu--horizontal > .el-menu-item {
    cursor: pointer;
    color: #333;
  }
  .nav-right {
    position: relative;
    padding-top: 15px;
    text-align: right;
    .el-dropdown {
      cursor: pointer;
      padding-right: 60px;
    }
    .user-img {
      position: absolute;
      top: -15px;
      right: 0;
      width: 50px;
      border-radius: 50%;
    }
  }
}

.enter-slideUp,
.leave-slideDown {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1010;
}

.enter-slideUp {
  overflow: auto;
  visibility: visible;
  z-index: 1001;
  animation: slideUp 0.3s forwards;
}
.leave-slideDown {
  visibility: visible;
  z-index: 1001;
  animation: slideDown 0.3s forwards;
}
@keyframes slideUp {
  from {
    transform: translate3d(0, 100%, 0);
    opacity: 0.1;
  }
  to {
    transform: translate3d(0, 0, 0);
    opacity: 1;
  }
}
@keyframes slideDown {
  from {
    transform: translate3d(0, 0, 0);
  }
  to {
    transform: translate3d(0, 100%, 0);
    opacity: 0;
  }
}
.mask {
  position: fixed;
  z-index: 100;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #000;
  opacity: 0.5;
}
.mask-fade-out {
  animation: maskFadeOut 0.4s forwards;
}
@keyframes maskFadeOut {
  from {
    opacity: 0.5;
  }
  to {
    opacity: 0;
  }
}



.top{
  padding: 15px 0;
  display: flex;
  justify-content: space-between;
  height: 5rem;
  width: 100%;
  color: #fff;
  position: relative;
  .name-btn{
    margin-left: 1.25rem;
    font-size: 2.1rem;
    font-weight: 600;
    text-decoration-color:transparent;
  }
  .menu-btn{
    margin-right: 3rem;
    line-height: 1.9rem;
    text-decoration-color:transparent;
    span:nth-child(1){
      color: #a8a39d;
      font-size: 1.8rem;
      font-weight: 400;
    }
    span:nth-child(2){
      color: #ffff00;
      font-size: 1.6rem;
      font-weight: 400;
    }
  }
  .menu-btn:hover {
    text-decoration: underline;
    text-decoration-color: #ffbc11; 
    text-decoration-thickness: 3px; 
    text-underline-offset: 8px;
    span:nth-child(1){
      color: white;
    }
  }
  .name-btn:hover {
    text-decoration: underline;
    text-decoration-color: #c06c84; 
    text-decoration-thickness: 3px; 
    text-underline-offset: 8px;
  }
}

.overlay {
  background-color: rgba(32, 36, 80);
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1001
}

.overlay::before {
  content: "isMenu()";
  font-size: 54vh;
  text-align: center;
  position: absolute;
  font-family: ui-serif, Georgia, Cambria, "Times New Roman", Times, serif;
  top: calc(50% - 45vh);
  left: 0;
  width: 100%;
  height: 100%;
  color: #f2f2f2; 
  opacity: 0.05; 
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
