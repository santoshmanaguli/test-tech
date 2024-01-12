<script>
import axios from 'axios';

export default {
  data() {
    return {
      posts: [],
      postComments: []
    }
  },
  methods: {
    getData() {
      axios.get('https://dummyjson.com/posts')
        .then(response => {
          console.log(response);
          let data = response.data.posts;
          this.posts = response.data.posts;
        })
        .catch(err => {
          console.log(err);
        })
    },
    getComments(id) {
      axios.get(`https://dummyjson.com/post/${id}/comments`)
        .then(response => {
          console.log(response);
          this.postComments = response.data.comments
        })
        .catch(err => {
          console.log(err);
        })
    }
  }
}
</script>

<template>
  <div>
    <button @click="getData()">
      Get Data
    </button>

    <table>
      <thead>
        <tr>
          <th>
            id
          </th>
          <th style="width:fit-content ;">
            user id
          </th>
          <th>
            title
          </th>
          <th>
            comment
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="post in posts" :key="post.id">
          <td>
            {{ post.id }}
          </td>
          <td>
            {{ post.userId }}
          </td>
          <td>
            {{ post.title }}
          </td>
          <td>
            {{ post.body }}
          </td>
          <td>
            <button v-if="post.comments == ''" @click="getComments(post.id)">
              View Comment
            </button>
            <div v-else>
              {{ post.comments }}
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style></style>