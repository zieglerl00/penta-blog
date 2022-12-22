<template>
  <div :key="post.id" v-for="post in posts" class="w-4/12 mx-auto shadow-lg p-3 rounded-lg mt-2 bg-slate-700 text-white">
    <p class="border-b-2 text-sm ">{{post.username}}</p>
    <p style="height: 100px" class="mt-2">{{post.blogContent}}</p>
  </div>
</template>

<script lang="ts">

import {ref} from "vue";

export default {
  setup() {
    const posts = ref()

    getPosts()
    function getPosts() {
      fetch("https://vue-http-demo-1cf5e-default-rtdb.europe-west1.firebasedatabase.app/posts.json")
          .then((response) => {
            if (response.ok) {
              return response.json()
            }
          }).then((data) => {
        const tmpPostsArr = []
        for (const id in data) {
          tmpPostsArr.push({id: id, username: data[id].username, blogContent: data[id].blogContent})
        }
        posts.value = tmpPostsArr
      })
    }

    return {
      posts
    }
  }
}
</script>