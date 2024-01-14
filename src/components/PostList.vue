<script>
import axios from 'axios';
import PostItem from './PostItem.vue';
import Comments from './Comments.vue';

export default {
  components: {
    PostItem,
    Comments,
  },
  data() {
    return {
      posts: [],
      selectedPostId: null,
      comments: [],
    };
  },
  created() {
    this.fetchPosts();
  },
  methods: {
    fetchPosts() {
      axios.get('https://dummyjson.com/posts')
        .then(response => {
          this.posts = response.data.posts;
          console.log(this.posts);
        })
        .catch(error => {
          console.error(error);
        });
    },
    fetchComments(postId) {
      this.selectedPostId = postId;
      axios.get(`https://dummyjson.com/posts/${postId}/comments`)
        .then(response => {
          this.comments = response.data.comments;
        })
        .catch(error => {
          console.error(error);
        });
    },
  },
};
</script>

<template>
  <div>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Title</th>
          <th>Body</th>
          <th>User ID</th>
          <th>Comments</th>
        </tr>
      </thead>
      <tbody>
        <post-item v-for="post in posts" :key="post.id" :post="post" @fetch-comments="fetchComments" />
      </tbody>
    </table>
    <comments v-if="selectedPostId" :comments="comments" />
  </div>
</template>

<style>
</style>