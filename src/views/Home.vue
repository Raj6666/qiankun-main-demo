<template>
  <div class="home">
    <p class="title">HelloWorld</p>
    <button @click="getHomeData()">请求首页数据</button>
    <button @click="updateHomeData()">更新首页数据</button><br />
    <button @click="getUserData()">请求用户数据</button>
    <img alt="Vue logo" src="../assets/images/logo.png" />
    <HelloWorld></HelloWorld>
    <div id="app-micro"></div>
  </div>
</template>

<script>
import {loadMicroApp} from 'qiankun';
// import {registerMicroApps, start} from 'qiankun';
export default {
  name: 'Home',
  components: {},
  data() {
    return {
      microApp: null,
    };
  },
  mounted() {
    // 获取应用配置并手动挂载，挂载后返回挂载对象
    this.microApp = loadMicroApp({
      name: 'vueMicroApp', // 应用的名字 必填 唯一
      entry: '//localhost:2040', // 默认会加载这个html 解析里面的js 动态的执行 （子应用必须支持跨域）fetch
      container: '#app-micro', // 挂载具体容器 ID
      // activeRule: '/user', // 根据路由 激活的子应用
      // props: {
      //   xxxx: '/', // 下发给子应用
      //   test: true
      // },
    });
    // registerMicroApps([
    //   {
    //     name: 'vueMicroApp', // 应用的名字 必填 唯一
    //     entry: '//localhost:2040', // 默认会加载这个html 解析里面的js 动态的执行 （子应用必须支持跨域）fetch
    //     container: '#app-micro', // 挂载具体容器 ID
    //     activeRule: '/', // 根据路由 激活的子应用
    //     props: {
    //       xxxx: '/', // 下发给子应用
    //     },
    //   },
    // ]);
    // start();
  },
  beforeUnmount() {
    this.microApp.unmount();
  },
  methods: {
    async getHomeData() {
      const result = await this.Api.home.getHomeList({name: '测试'});
      console.log(result);
    },
    async updateHomeData() {
      const result = await this.Api.home.updateHomeList({name: '测试'});
      console.log(result);
    },
    async getUserData() {
      const result = await this.Api.userModule.getUser({name: '测试'});
      console.log(result);
    },
  },
};
</script>

<style lang="scss" scoped>
.title {
  color: red;
  @include transform-centering;
}
</style>
