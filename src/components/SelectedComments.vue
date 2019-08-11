<template lang="html">
  <div class="">
  <ul>
    <li v-for="comment in comments.slice(1)">{{comment.data.body}}</li>
  </ul>
</div>

</template>

<script>
export default {
  name: 'selected-comments',
  props: ['comments']

  // computed: {
  //   results: function () {
  //     const assholes = {YTA: 0, NTA: 0, ESH: 0, NAH: 0};
  //     for (comment in comments.slice(1)) {
  //       if (comment.data.body.includes(YTA)) {
  //         assholes.YTA += 1
  //       } else if (comment.data.body.includes(NTA)) {
  //         assholes.NTA += 1
  //       } else if (comment.data.body.inlcudes(ESH)) {
  //         assholes.ESH += 1
  //       } else {
  //         assholes.NAH +=1
  //       }
  //     }
  //     return assholes
  //   }
  // }

}
</script>

<style lang="css" scoped>
</style>
