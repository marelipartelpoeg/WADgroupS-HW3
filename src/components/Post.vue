<template>
  <div class="post">
    <div class="header">
      <img class="profile-picture" :src="post.profilePicture" alt="Profile picture">
      <p>{{ post.date }}</p>
    </div>
    <div class="post-content">
      <img class="image" :src="post.picture" alt="Post image" v-if="post.picture">

      <p>{{ post.text }}</p>

      <button class="like-button" @click="toggleLike"></button>
      <span class="like-count">{{ post.likes }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: Object // Receive a post object from the parent component
  },
  data() {
    return {
      isLiked: this.post.liked || false // Track the liked state of the post
    };
  },
  methods: {
    toggleLike() {
      if (this.isLiked) {
        this.isLiked = false;
        this.post.likes++;
      } else {
        this.isLiked = true;
        this.post.likes++;
      }
    }
  },
}
</script>

<style scoped>
.post {
  border-radius: 25px;
  border: 2px solid #2a2cc9;
  background-color: rgb(231, 231, 231);
  margin: 50px;
  width: 350px;
  padding: 20px;
  padding-bottom: 5px;
}

.header {
  display: flex;
  align-items: center;
  gap: 170px;
}

.header img {
  width: 30px;
  height: 30px;
}

.image {
  width: 300px;
}

.like-count {
  font-weight: bold;
  margin-left: 10px;
}

.like-button {
  background-image: url('/public/like.png');
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
  background-color: rgb(231, 231, 231);
  width: 30px;
  height: 30px;
  border: none;
  cursor: pointer;
}
</style>
