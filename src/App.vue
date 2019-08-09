<template lang="html">
  <div class="">
    <select-post :posts="posts"/>
    <button type="button" @click="getLatest">Get latest</button>
    <full-post :post="selectedPost"/>
  </div>
</template>

<script>
import { eventBus } from '@/main.js'
import SelectPost from './components/PostSelect'
import FullPost from './components/FullPost'

export default {
  data(){
    return {
      posts: [],
      selectedPost: null
    }
  },

  mounted() {
    eventBus.$on('post-selected', (index) => {
      this.selectedPost = this.posts[index];
    })
    getLatest()



    // fetch('https://www.reddit.com/r/AmItheAsshole/top/.json')
    //   .then(res => res.json())
    //   .then(returnedData => this.posts = returnedData.data.children)
  },

  components: {
    "select-post": SelectPost,
    "full-post": FullPost
  },

  methods: {
   getLatest(){
     fetch('https://www.reddit.com/r/AmItheAsshole/top/.json')
       .then(res => res.json())
       .then(returnedData => this.posts = returnedData.data.children)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
