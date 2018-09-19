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
    </div>
    <Footer></Footer>
  </div>
</template>
<script>
  import Header from '../components/header.vue'
  import Footer from '../components/footer.vue'
  export default {
    components: { Header, Footer },
    data () {
      return {
        list: []
      }
    },
    created () {
      this.getData()
    },
    methods: {
      getData () {
        this.$api.get('article/all', null, r => {
          this.list = r
          console.log(r)
        })
      }
    }
  }
</script>
