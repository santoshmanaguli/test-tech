<script>
export default {
  props: {
    comments: Array,
  },
};
</script>

<template>
  <div>
    <h2>Comments</h2>
    <ul>
      <li v-for="comment in comments" :key="comment.id">{{ comment.body }}</li>
    </ul>
  </div>
</template>
