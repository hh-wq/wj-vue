<template>
    <div>
      <el-row style="height: 840px;">
        <search-bar @onSearch="search" ref="searchBar"></search-bar>
        <el-tooltip effect="dark" placement="right"
                    v-for="item in books.slice((currentPage-1)*pageSize,currentPage*pageSize)"
                    :key="item.id">
          <p slot="content" style="font-size: 14px;margin-bottom: 6px;">{{item.title}}</p>
          <p slot="content" style="font-size: 13px;margin-bottom: 6px">
            <span>{{item.author}}</span> /
            <span>{{item.date}}</span> /
            <span>{{item.press}}</span>
          </p>
          <p slot="content" style="width: 300px" class="abstract">{{item.abs}}</p>
          <el-card style="width: 135px;margin-bottom: 20px;height: 233px;float: left;margin-right: 15px" class="book"
                   bodyStyle="padding:10px" shadow="hover">
            <div class="cover">
              <img :src="item.cover" alt="封面">
            </div>
            <div class="info">
              <div class="title">
                <a href="">{{item.title}}</a>
              </div>
            </div>
            <div class="author">{{item.author}}</div>
          </el-card>
        </el-tooltip>
      </el-row>
      <el-row>
        <el-pagination
          :current-page="currentPage"
          :page-size="pageSize"
          :total="20">
        </el-pagination>
      </el-row>
    </div>
  </template>

<script>
import SearchBar from './SearchBar'
export default {
  name: 'Books',
  components: {SearchBar},
  data () {
    return {
      books: [],
      currentPage: 1,
      pageSize: 15
    }
  },
  mounted: function () {
    this.loadBooks()
  },
  methods: {
    loadBooks () {
      var _this = this
      this.$axios.get('/books').then(response => {
        if (response && response.status === 200) {
          _this.books = response.data
        }
      })
    },
    search () {
      var _this = this
      this.$axios.get('/search?keywords=' + this.$refs.searchBar.keywords).then(response => {
        if (response && response.status === 200) {
          _this.books = response.data
        }
      })
    }
  }
}

</script>

  <style scoped>
    .cover {
      width: 115px;
      height: 172px;
      margin-bottom: 7px;
      overflow: hidden;
      cursor: pointer;
    }

    img {
      width: 115px;
      height: 172px;
      /*margin: 0 auto;*/
    }

    .title {
      font-size: 14px;
      text-align: left;
    }

    .author {
      color: #333;
      width: 102px;
      font-size: 13px;
      margin-bottom: 6px;
      text-align: left;
    }

    .abstract {
      display: block;
      line-height: 17px;
    }

    a {
      text-decoration: none;
    }

    a:link, a:visited, a:focus {
      color: #3377aa;
    }
  </style>
