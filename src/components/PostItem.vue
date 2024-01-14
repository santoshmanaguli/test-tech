<script>
export default {
  props: {
    post: Object,
  },
};
</script>

<template>
  <tr>
    <td>{{ post.id }}</td>
    <td>{{ post.title }}</td>
    <td>{{ post.body }}</td>
    <td>{{ post.userId }}</td>
    <td><button @click="$emit('fetch-comments', post.id)">Fetch Comments</button></td>
  </tr>
</template>
