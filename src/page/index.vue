<template>
  <div>
    <Header></Header>
    <div class="article_list">
      <ul>
        <li v-for="i in list">
          <time v-text="i.date"></time>
          <router-link :to="'/content/' + i.id">
            {{ i.title }}
          </router-link>
          <article v-text="i.summary"></article>
        </li>
      </ul>
      <mo-paging
        :page-index="currentPage"
        :total="count"
        :page-size="pageSize"
        @change="pageChange">
      </mo-paging>
    </div>
    <Footer></Footer>
  </div>
</template>
<style src="../style/scss/_paging.scss" lang="scss">
</style>
<script>
  import Header from '../components/header.vue'
  import Footer from '../components/footer.vue'
  import MoPaging from '../components/paging.vue'

  export default {
    components: { Header, Footer, MoPaging },
    data () {
      return {
        pageSize : 10 , //每页显示20条数据
        currentPage : 1, //当前页码
        count : 0, //总记录数
        list: []
      }
    },
    created () {
      this.getData()
    },
    methods: {
      getData () {
        this.$api.get('article/all?pageSize=' + this.pageSize + '&currentPage=' + this.currentPage, null, r => {
          this.list = r.resData
          this.count = r.count
        })
      },
      //从page组件传递过来的当前page
      pageChange (page) {
        this.currentPage = page
        this.getData()
      }
    }
  }
</script>
