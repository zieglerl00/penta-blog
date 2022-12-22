<template>
<blog-base></blog-base>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BlogBase from "@/components/BlogBase.vue";

export default defineComponent({
  name: 'App',
  components: {
    BlogBase
  }
});
</script>

<style>
body {
  background: #060D0D;
  background-attachment: fixed;
}

</style>
