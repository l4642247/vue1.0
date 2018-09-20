<template>
  <div>
    <myHeader></myHeader>
    <h2 v-text="article.title"></h2>
    <p v-text="article.date"></p>
    <hr>
    <article v-html="article.content"></article>
    <myFooter></myFooter>
  </div>
</template>
<script>
  import myHeader from '../components/header.vue'
  import myFooter from '../components/footer.vue'
  export default {
    components: { myHeader, myFooter },
    data () {
      return {
        id: this.$route.params.id,
        article: {}
      }
    },
    created () {
      this.getData()
    },
    methods: {
      getData () {
        this.$api.get('article/content/' + this.id, null, r => {
          this.article = r.resData
        })
      }
    }
  }
</script>
