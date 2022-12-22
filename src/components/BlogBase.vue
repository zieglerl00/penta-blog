<template>
  <new-post></new-post>
  <all-posts></all-posts>
</template>

<script>
import NewPost from "@/components/NewPost.vue";
import AllPosts from "@/components/AllPosts.vue";

export default {
  components: {AllPosts, NewPost}

}
</script>