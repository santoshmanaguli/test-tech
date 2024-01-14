<script>
export default {
  props: {
    comments: Array,
  },
};
</script>

<template>
  <section id="comments">
    <h2>Comments Section</h2>
    <ul>
      <li v-for="comment in comments" :key="comment.id">{{ comment.body }}</li>
    </ul>
  </section>
</template>
