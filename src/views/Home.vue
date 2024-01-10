<template>
  <div class="home">
    <canvas id="sakura" />
    <div class="content">
      <div class="home-header">
        <router-link
          class="link"
          to="/"
        >
          <img
            class="home-logo"
            src="../assets/userLogo.jpg"
            alt="biaochenxuying logo"
          />
        </router-link>
      </div>
      <div class="home-body">
        <div class="list">
          <router-link
            class="link"
            to="/test"
          >
            效果
          </router-link>
          <router-link
            class="link"
            to="/articles"
          >
            文章
          </router-link>
          <router-link
            class="link"
            to="/project"
          >
            项目
          </router-link>
          <a
            target="_blank"
            rel="noopener noreferrer"
            class="link"
            href="https://github.com/biaochenxuying"
          >
            github
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted } from "vue";
import { ElMessage } from "element-plus";

export default defineComponent({
  name: "Home",

});
</script>

<style lang="less" scoped>
.home {
  position: fixed;
  left: 0;
  top: 0;
  .content {
    position: fixed;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    font-size: 20px;
    text-align: center;
    padding-top: 12%;
    height: 100%;
    background-image: url("../assets/bg.png");
    background-size: cover;
    .home-logo {
      width: 220px;
      border-radius: 70%;
      animation: mylogo 6s;
      -moz-animation: mylogo 6s; /* Firefox */
      -webkit-animation: mylogo 6s; /* Safari and Chrome */
      -o-animation: mylogo 6s; /* Opera */
      animation-iteration-count: infinite;
    }
    .home-header {
      .link {
        display: block;
      }
    }
    .home-body {
      padding-top: 20px;
      .list {
        .link {
          display: inline-block;
          padding: 20px;
          color: pink;
          min-width: 80px;
        }
        .link:hover {
          color: orange;
        }
      }
    }
    .introduce {
      padding-top: 20px;
      color: #fff;
    }
  }
}
@keyframes mylogo {
  0% {
    transform: rotate(0deg) scale(0.8, 0.8);
    opacity: 1;
  }
  25% {
    transform: rotate(0deg) scale(1, 1);
    opacity: 0.8;
  }
  100% {
    transform: rotate(0deg) scale(0.8, 0.8);
    opacity: 1;
  }
}

@-moz-keyframes mylogo {
  0% {
    transform: rotate(0deg) scale(0.8, 0.8);
    opacity: 1;
  }
  25% {
    transform: rotate(0deg) scale(1, 1);
    opacity: 0.8;
  }
  100% {
    transform: rotate(0deg) scale(0.8, 0.8);
    opacity: 1;
  }
}

@-webkit-keyframes mylogo {
  0% {
    transform: rotate(0deg) scale(0.8, 0.8);
    opacity: 1;
  }
  25% {
    transform: rotate(0deg) scale(1, 1);
    opacity: 0.8;
  }
  100% {
    transform: rotate(0deg) scale(0.8, 0.8);
    opacity: 1;
  }
}

@-o-keyframes mylogo {
  0% {
    transform: rotate(0deg) scale(0.8, 0.8);
    opacity: 1;
  }
  25% {
    transform: rotate(0deg) scale(1, 1);
    opacity: 0.8;
  }
  100% {
    transform: rotate(0deg) scale(0.8, 0.8);
    opacity: 1;
  }
}
</style>

