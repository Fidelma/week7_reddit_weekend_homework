<template lang="html">
  <ul>
    <li v-for="comment in comments">{{comment.data.body}}</li>
  </ul>

</template>

<script>
export default {
  name: 'selected-comments',
  props: ['comments']
}
</script>

<style lang="css" scoped>
</style>
