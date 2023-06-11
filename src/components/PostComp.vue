<template>
  <div class="post">
    <div class="post-header">
      <div
        class="profile"
        :style="{ backgroundImage: `url(${content.userImage})` }"
      ></div>
      <span class="profile-name">{{ content.name }}</span>
    </div>
    <div
      class="post-body"
      :style="{ backgroundImage: `url(${content.postImage})` }"
    ></div>
    <div class="post-content">
      <p>{{ content.likes }} Likes</p>
      <p>
        <strong>{{ content.name }}</strong
        >{{ content.content }}
      </p>
      <p class="date">{{ content.date }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "PostComp",
  props: {
    content: Object,
  },
};
</script>

<style></style>
