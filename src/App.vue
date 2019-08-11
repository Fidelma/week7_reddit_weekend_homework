<template lang="html">
  <div class="">
    <p>{{this.result}}</p>
    <select-post :posts="posts"/>
    <button type="button" @click="getLatest">Get latest</button>
    <p v-if="selectedPost">Verdict: {{selectedPost.data.link_flair_text}}</p>
    <full-post :post="selectedPost"/>
    <button v-if="selectedPost" type="button" @click="seen = !seen">Comments</button>
    <button v-if="selectedPost" type="button" @click="results">Ratios</button>
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
      seen: false,
      result: {YTA: 0, NTA: 0, ESH: 0, NAH: 0}
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

    // computed: {

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
    },

    results() {
      // console.log(this.comments[1].data.body.toString().includes('NTA'));
      // const assholes = {YTA: 0, NTA: 0, ESH: 0, NAH: 0};
      // for (var comment in this.comments.slice(1)) {
      //   console.log(comment);
      // }
      this.comments.slice(1).forEach((comment)=> {
        console.log(comment.data.body.toString().includes('y'));
        // if (comment.data.body.toString().includes('YTA')) {
        //   console.log(comment);
        //   this.result.YTA += 1
        // } else if (comment.data.body.toString().includes('NTA')) {
        //   this.result.NTA += 1
        // } else if (comment.data.body.toString().inlcudes('ESH')) {
        //   this.result.ESH += 1
        // } else {
        //   this.result.NAH +=1
        // }
    })
    // return assholes
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
