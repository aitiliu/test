<!-- components/PostList.vue -->
<template>
  <div>
    <h1>Posts</h1>
    <ul>
      <li v-for="post in posts" :key="post.id">{{ post.title }}</li>
    </ul>
  </div>
</template>

<script lang="ts">
import { storeToRefs } from "pinia";
import { usePostsStore } from '@/store'
import { onMounted, onBeforeMount } from 'vue'



export default {
  setup() {
    const postsStore = usePostsStore()
    const { posts } = storeToRefs(postsStore);

    onBeforeMount(async () => {
      await postsStore.fetchPosts()
    })

    return {
      posts: postsStore.posts
    }
  }
}
</script>