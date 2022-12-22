<template>
  <form @submit.prevent="sendBlogPost" class="flex flex-col w-4/12 mx-auto mb-5">
    <input class="border p-2 rounded-lg shadow-lg my-5 text-white" style="background: rgba(6,13,13,0)" v-model="username" type="text" placeholder="Username">
    <textarea rows="5" cols="10" style="background: rgba(6,13,13,0)" class="border p-2 rounded-lg shadow-lg mb-5 text-white" v-model="text"></textarea>
    <h3 v-if="!valid" class="text-red-600 mx-auto mb-5">Please fill out everything</h3>
    <h3 v-if="sendedSuccessfull" class="text-green-600 mx-auto mb-5">Posted</h3>
    <button
        class="bg-sky-400 p-2 rounded-lg shadow-lg text-white font-bold text-lg hover:bg-sky-500 transition ease-in-out duration-100">
      Send
    </button>
  </form>

</template>

<script lang="ts">
import {ref, watch} from "vue";

export default {
  setup() {
    const username = ref<string>("")
    const text = ref<string>("")
    const valid = ref<boolean>(true)
    const sendedSuccessfull = ref<boolean>(false)

    function sendBlogPost() {
      if (username.value.length === 0 || text.value.length === 0) {
        valid.value = false
      }
      if (valid.value === true) {
        fetch("https://vue-http-demo-1cf5e-default-rtdb.europe-west1.firebasedatabase.app/posts.json", {
          method: "POST",
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            username: username.value,
            blogContent: text.value
          })
        }).then((response) => {
          if (response.ok) {
            text.value = ""
            username.value = ""
            sendedSuccessfull.value = true
          }
        })
      }
    }

    watch([username, text], (currentValues) => {
      if (currentValues[0].length !== 0 && currentValues[1].length !== 0) {
        valid.value = true
      }
    })

    return {
      username,
      text,
      sendBlogPost,
      valid,
      sendedSuccessfull
    }
  }
}
</script>