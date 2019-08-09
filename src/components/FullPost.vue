<template lang="html">
  <div v-if="post">
   <h2>{{post.data.title}}</h2>
   <p>{{post.data.selftext}}</p>
  </div>
</template>

<script>
export default {
  name: "full-post",
  props: ['post']
}
</script>

<style lang="css" scoped>
</style>
