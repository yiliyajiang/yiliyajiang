<template>
  <MouseStarFollow>
    <div class="main_container">
      <div class="video-bg">
        <video width="320" height="240" autoplay loop muted>
          <source src="./assets/background-image.mp4" type="video/mp4" />
          Your browser does not support the video tag.
        </video>
      </div>

      <div class="main">
        <!--顶部导航栏菜单-->
        <header-component></header-component>

        <div class="wrapper">
          <!--左边导航栏菜单-->
          <left-component></left-component>
          <!-- 内容区域 -->
          <router-view></router-view>
        </div>
      </div>
    </div>
  </MouseStarFollow>
</template>

<script>
import HeaderComponent from "@/components/HeaderComponent";
import LeftComponent from "@/components/LeftComponent";
import MouseStarFollow from "@/views/star/StarView.vue";

export default {
  name: "App",
  components: { MouseStarFollow, HeaderComponent, LeftComponent },
  data() {
    return {};
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700&display=swap");

#app {
  display: grid;
  width: 100vw;
  height: 100vh;
}

/*背景视频*/
.video-bg {
  position: fixed;
  right: 0;
  top: 0;
  width: 100%;
  height: 100%;
}

video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/*主页面*/
.main {
  background-color: rgba(16 18 27 / 30%);
  max-width: 1200px;
  max-height: 860px;
  height: 90vh;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  position: relative;
  width: 100%;
  border-radius: 14px;
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  font-size: 15px;
  font-weight: 500;
}
.wrapper {
  display: flex;
  flex-grow: 1;
  overflow: auto !important;
}

/*浏览器滚动条样式*/
::-webkit-scrollbar {
  width: 6px;
  border-radius: 10px;
  background: -webkit-linear-gradient(top, #db6ff3 0%, rgb(240, 240, 103) 100%);
}

::-webkit-scrollbar-thumb {
  border-radius: 10px;
  background: -webkit-linear-gradient(top, #f16de4 0%, rgba(83, 237, 142, 0) 100%);
}

.main_container {
  display: grid;
  width: 1300px;
  margin: auto;
}
@media screen and (max-width: 1300px) {
  .main_container {
    width: 100vw;
    height: 100vh;
    display: grid;
  }
  .main {
    height: auto;
    max-width: none;
    max-height: none;
  }
}
.wrapper {
  position: relative;
}
body p {
  margin: 0;
}
</style>
