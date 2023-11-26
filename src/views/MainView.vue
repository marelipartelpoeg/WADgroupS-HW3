<template>
  <div class="post-container">
    <post v-for="post in postList" :key="post.id" :post="post"></post>
  </div>
  <div class="reset-likes">
    <button @click="resetLikes">Reset likes</button>
  </div>
</template>

<script>
import Post from "@/components/Post.vue";

export default {
  components: {
    Post
  },
  methods: {
    resetLikes() {
      this.postList.forEach(post => post.likes = 0);
    }
  },
  computed: {
    postList() {
      return this.$store.state.postList
    }
  }
}
</script>

<style scoped>
.post-container {
  display: flex;
  align-items: center;
  flex-direction: column;
}

.reset-likes {
  position: sticky;
  bottom: 0;
}
</style>