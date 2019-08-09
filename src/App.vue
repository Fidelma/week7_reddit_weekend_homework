<template lang="html">
  <div class="">
    <select-post :posts="posts"/>
    <button type="button" @click="getLatest">Get latest</button>
    <full-post :post="selectedPost"/>
    <button v-if="selectedPost" type="button" @click="">View Comments</button>
    <selected-comments v-if="comments" :comments="comments"/>
  </div>
</template>

<script>
import { eventBus } from '@/main.js'
import SelectPost from './components/PostSelect'
import FullPost from './components/FullPost'
import SelectedComments from './components/SelectedComments'

export default {
  data(){
    return {
      posts: [],
      selectedPost: null,
      comments: []
    }
  },

  mounted() {
    eventBus.$on('post-selected', (index) => {
      this.selectedPost = this.posts[index];
    })
    this.getLatest()



    // fetch('https://www.reddit.com/r/AmItheAsshole/top/.json')
    //   .then(res => res.json())
    //   .then(returnedData => this.posts = returnedData.data.children)
  },
  computed: {
    seeComments(){
      const commentsURL = this.selectedPost.data.url
      const jsonCommentsURL = commentsURL + '.json'
      fetch(jsonCommentsURL)
        .then(res => res.json())
        .then(comments => this.comments = comments[1].data.children)
    }
  },

  components: {
    "select-post": SelectPost,
    "full-post": FullPost,
    "selected-comments": SelectedComments
  },

  methods: {
   getLatest(){
     fetch('https://www.reddit.com/r/AmItheAsshole/top/.json')
       .then(res => res.json())
       .then(returnedData => this.posts = returnedData.data.children)
    },

    // seeComments(){
    //   const commentsURL = this.selectedPost.data.url
    //   const jsonCommentsURL = commentsURL + '.json'
    //   fetch(jsonCommentsURL)
    //     .then(res => res.json())
    //     .then(comments => this.comments = comments[1].data.children)
    // }
  }
}
</script>

<style lang="css" scoped>
</style>
