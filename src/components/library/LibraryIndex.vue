<template>
    <el-container>
        <el-aside style="width: 200px;margin-top: 20px">
            <SideMenu @CategoryChange="listByCategory" ref="sideMenu"></SideMenu>
        </el-aside>
        <el-main>
            <Books class="books-area" ref="booksArea"></Books>
        </el-main>
    </el-container>
</template>

<script>
import SideMenu from './SideMenu'
import Books from './Books'
export default {
  name: 'AppLibrary',
  components: {SideMenu, Books},
  methods: {
    listByCategory () {
      var _this = this
      var cid = this.$refs.sideMenu.cid
      var url = '/categories/' + cid + '/books'
      this.$axios.get(url).then(response => {
        if (response && response.status === 200) {
          _this.$refs.booksArea.books = response.data
        }
      })
    }
  }
}
</script>

<style scoped>
</style>
