<script>
import axios from "axios";
import PostItem from "./PostItem.vue";
import Comments from "./Comments.vue";

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
      axios
        .get("https://dummyjson.com/posts")
        .then((response) => {
          this.posts = response.data.posts;
          console.log(this.posts);
        })
        .catch((error) => {
          console.error(error);
        });
    },
    fetchComments(postId) {
      this.selectedPostId = postId;
      axios
        .get(`https://dummyjson.com/posts/${postId}/comments`)
        .then((response) => {
          this.comments = response.data.comments;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<template>
  <div class="table-border-div table-responsive">
    <table class="table table-hover align-middle">
      <thead>
        <tr class="text-center">
          <th>ID</th>
          <th>Title</th>
          <th style="width: 70%">Body</th>
          <th>UID</th>
          <th>Comments</th>
        </tr>
      </thead>
      <tbody class="table-group-divider">
        <post-item
          v-for="post in posts"
          :key="post.id"
          :post="post"
          @fetch-comments="fetchComments"
        />
      </tbody>
    </table>
    <comments v-if="selectedPostId" :comments="comments" />
  </div>
</template>

<style scoped>
.table-border-div {
  padding: 0px 10px 0px 10px;
}
</style>
