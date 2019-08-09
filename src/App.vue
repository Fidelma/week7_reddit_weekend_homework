<template lang="html">
  <div class="">
    <select-post :posts="posts"/>
    <button type="button" @click="getLatest">Get latest</button>
    <p v-if="selectedPost">Verdict: {{selectedPost.data.link_flair_text}}</p>
    <full-post :post="selectedPost"/>
    <button v-if="selectedPost" type="button" @click="seen = !seen">Comments</button>
    <selected-comments v-if="seen" :comments="comments"/>
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
      comments: [],
      seen: false
    }
  },

  mounted() {
    eventBus.$on('post-selected', (index) => {
      this.selectedPost = this.posts[index];
      this.seeComments();
    })
    this.getLatest()



    // fetch('https://www.reddit.com/r/AmItheAsshole/top/.json')
    //   .then(res => res.json())
    //   .then(returnedData => this.posts = returnedData.data.children)
  },
  computed: {
    // seeComments(){
    //   const commentsURL = this.selectedPost.data.url
    //   const jsonCommentsURL = commentsURL + '.json'
    //   fetch(jsonCommentsURL)
    //     .then(res => res.json())
    //     .then(comments => this.comments = comments[1].data.children)
    // }
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

    seeComments(){
      const commentsURL = this.selectedPost.data.url
      const jsonCommentsURL = commentsURL + '.json'
      fetch(jsonCommentsURL)
        .then(res => res.json())
        .then(comments => this.comments = comments[1].data.children)
    }

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
