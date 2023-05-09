<template>
  <div>
    <!-- 头部标题区域 -->
    <!-- logo区域 -->
    <div class="header" v-if="showHeader">
      <div class="header-content" :style="{width: proxy.globalInfo.bodywidth + 'px'}">
        <router-link to="/" class="logo">
          <span v-for="item in logoInfo" :style="{color: item.color}">{{ item.letter }}</span>
        </router-link>
        <!-- 菜单导航栏 -->
        <div class="menu-panel"></div>
        <!-- 用户信息注册登录 -->
        <div class="user-info-panel">
          <div class="op-btn">
            <el-button type="primary" >发帖
              <span class="iconfont icon-add"></span>
            </el-button>
            <el-button type="primary" >搜索
              <span class="iconfont icon-search"></span>
            </el-button>
          </div>
        
          <el-button-group :style="{'margin-left': '10px'}">
            <el-button type="primary" plain>注册</el-button>
            <el-button type="primary" plain>登录</el-button>
          </el-button-group>
        </div>
      </div> 
    </div>
    <div class="main">
      
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, getCurrentInstance, onMounted } from "vue"
import { useRouter, useRoute } from "vue-router";
const { proxy } = getCurrentInstance()
const router = useRouter()
const route = useRoute()

const logoInfo = ref([
  {
    letter: "E",
    color: "#3285FF"
  },
  {
    letter: "a",
    color: "#FB3624"
  },
  {
    letter: "s",
    color: "#FFBA02"
  },
  {
    letter: "y",
    color: "#3285ff"
  },
  {
    letter: "B",
    color: "#25b24e"
  },
  {
    letter: "B",
    color: "#fd3224"
  },
  {
    letter: "S",
    color: "#ffba02"
  },

])
//页面滑动控制header的显示与隐藏
const showHeader = ref(true)
//获取滚动条的高度
const getScrollTop = () => {
  let scrollTop =
    document.documentElement.scrollTop ||
    window.pageYOffset ||
    document.body.scrollTop
    return scrollTop

}

const initScroll = () => {
  let initScrollTop = getScrollTop()
  let scrollType = 0
  window.addEventListener('scroll', () => {
    let currentScrllTop = getScrollTop()
    if (currentScrllTop > initScrollTop) {
      //页面向下滑动
      scrollType = 1
    }
    else {
      //页面向上滑动
      scrollType = 0
    }
    initScrollTop = currentScrllTop
    if (scrollType === 1 && currentScrllTop > 100) {
      showHeader.value = false
    }
    else {
      showHeader.value = true
    }
    console.log(scrollType);
  })
}

onMounted(() => {
  initScroll()
})
</script>

<style lang="scss" scoped>
.header {
  width: 100%;
  height: 60px;
  position: fixed;
  box-shadow: 0 2px 6px 0 #ddd;
  z-index: 1000;
  background: #fff;
  .header-content{
    margin: 0px auto;
    align-items: center;
    height: 60px;
    display: flex;
    align-items: center;
    .logo{
      display: block;
      margin-right: 5px;
      text-decoration: none;
      span{
        font-size: 35px;
      }
    }
    .menu-panel{
      flex: 1;
    }
    .user-info-panel{
      display: flex;
      width: 310px;
      .op-btn{
        .iconfont{
          margin-left: 5px;
        }
        .el-button+.el-button {
        margin-left: 5px;
      }
      }
      
    }
  }
}
</style>
