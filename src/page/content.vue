<template>
  <div>
    <myHeader></myHeader>
    <!--<h2 v-text="dat.title"></h2>
    <p v-text="dat.date"></p>
    <hr>
    <article v-html="dat.content"></article>-->
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
        dat: {}
      }
    },
    created () {
      this.getData()
    },
    methods: {
      getData () {
        this.$api.get('article/content/' + this.id, null, r => {
          this.dat = r
          console.log(dat)
        })
      }
    }
  }
</script>
