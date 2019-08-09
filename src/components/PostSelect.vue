<template lang="html">
  <select @change="postSelected">
    <option selected disabled>-</option>
    <option v-for="(post, index) in posts" :value="index">{{post.data.title}}</option>
  </select>

</template>

<script>
import { eventBus } from '@/main.js';
export default {
  name: 'select-post',
  props: ['posts'],
  methods: {
    postSelected(e) {
      const selectedIndex = e.target.value;
      eventBus.$emit('post-selected', selectedIndex);
    }
  }
}
</script>

<style lang="css" scoped>

select {
  width: 50%;
}
</style>
