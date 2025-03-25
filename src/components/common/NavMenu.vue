<template>
<div>
    <el-menu
    :default-active="activeIndex"
    class="el-menu-demo"
    mode="horizontal"
    @select="handleSelect"
    background-color="white"
    text-color="#222"
    active-text-color="red"
    router>
    <el-menu-item v-for="(item, i) in navList" :key="i" :index="item.name">
        {{item.navItem}}
    </el-menu-item>
    <a href="#nowhere" style="color: #222;float: right;padding: 20px;">更多功能</a>
    <i class="el-icon-menu" style="float:right;font-size: 45px;color: #222;padding-top: 8px"></i>
    <span style="position: absolute;padding-top: 20px;right: 43%;font-size: 20px;font-weight: bold">White Jotter - Your Mind Palace</span>
    </el-menu>
</div>
</template>

<script>
export default {
  data () {
    return {
      activeIndex: '/index',
      navList: [
        {
          name: '/index',
          navItem: '首页'
        },
        {
          name: '/jotter',
          navItem: '笔记本'
        },
        {
          name: '/library',
          navItem: '图书馆'
        },
        {
          name: '/admin',
          navItem: '个人中心'
        }
      ]
    }
  },
  created () {
    // 初始化时根据当前路由设置激活项
    this.activeIndex = this.$route.path
  },
  watch: {
    '$route.path' (newVal) {
      // 路由变化时同步更新激活项
      this.activeIndex = newVal
    }
  }
}
</script>

<style scoped>
  a{
    text-decoration: none;
  }

  span {
    pointer-events: none;
  }
</style>
