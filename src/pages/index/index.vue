<template>
  <div class="container">
    <!-- 主页面路由 -->
    <div v-show="active == 0">
      <home />
    </div>
    <div v-show="active == 1">
      <application />
    </div>
    <div v-show="active == 2">
      <mine />
    </div>

    <!-- 底部标签栏 -->
    <van-tabbar :active="active" @change="onChange" z-index="9" active-color="#19be6b" inactive-color="#b2b2b2">
      <van-tabbar-item :name="0" icon="wap-home">首页</van-tabbar-item>
      <van-tabbar-item :name="1" icon="apps-o">功能</van-tabbar-item>
      <van-tabbar-item :name="2" icon="contact" info="5">我的</van-tabbar-item>
    </van-tabbar>
  </div>
</template>

<script>
import home from '@com/main/home.vue'
import application from '@com/main/application.vue'
import mine from '@com/main/mine.vue'
import {wxSetNavigationBarTitle} from '@/wx/index'
export default {
  components: {
    home,
    application,
    mine
  },
  data() {
    return {
      active: 2
    }
  },
  computed: {
    //监听active 动态设置导航标题
    watchActive() {
      if(this.active == 0) {
        wxSetNavigationBarTitle('首页')
      } else if(this.active == 1) {
        wxSetNavigationBarTitle('功能')
      } else if(this.active == 2) {
        wxSetNavigationBarTitle('我的')
      }
      return this.active
    }
  },
  methods: {
    // 点击底部栏
    onChange(e) {
      this.active = e.mp.detail
    }
  },
}

</script>

<style lang="scss" scope>
.container {
  margin-bottom: 50px;
  display: flex;
  flex-direction: column;
}
</style>
