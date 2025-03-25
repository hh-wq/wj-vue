<template>
    <el-container>
        <el-aside style="width: 200px;margin-top: 20px">
            <SideMenu></SideMenu>
        </el-aside>
        <el-main>Main</el-main>
    </el-container>
</template>

<script>
import SideMenu from './SideMenu'
export default {
  name: 'AppLibrary',
  components: {SideMenu}
}
</script>

<style scoped>
</style>
