<template>
  <div>
    <div v-if="tab === 0">
      <PostComp v-for="(content, idx) in data" :key="idx" :content="content" />
    </div>

    <!-- 필터선택페이지 -->
    <div v-if="tab === 1">
      <div
        class="upload-image"
        :style="{ backgroundImage: `url(${imgUrl})`, objectFit: 'contain' }"
      ></div>
      <div class="filters">
        <FilterBox
          v-for="(filter, idx) in filterList"
          :key="idx"
          :filter="filter"
          :imgUrl="imgUrl"
        />
      </div>
    </div>

    <!-- 글작성페이지 -->
    <div v-if="tab === 2">
      <div
        class="upload-image"
        :style="{ backgroundImage: `url(${imgUrl})` }"
      ></div>
      <div class="write">
        <textarea
          @input="$emit('write', $event.target.value)"
          class="write-box"
        >
        write!</textarea
        >
      </div>
    </div>
  </div>
</template>

<script>
import PostComp from "./PostComp.vue";
import FilterBox from "./FilterBox.vue";

export default {
  name: "ContainerComp",
  data() {
    return {
      filterList: [
        "aden",
        "_1977",
        "brannan",
        "brooklyn",
        "clarendon",
        "earlybird",
        "gingham",
        "hudson",
        "inkwell",
        "kelvin",
        "lark",
        "lofi",
        "maven",
        "mayfair",
        "moon",
        "nashville",
        "perpetua",
        "reyes",
        "rise",
        "slumber",
        "stinson",
        "toaster",
        "valencia",
        "walden",
        "willow",
        "xpro2",
      ],
    };
  },
  props: {
    data: Array,
    tab: Number,
    imgUrl: String,
    content: String,
  },
  components: {
    PostComp,
    FilterBox,
  },
  mounted() {
    console.log(this.imgUrl);
  },
};
</script>

<style>
.post {
  width: 100%;
}
.profile {
  background-image: url("https://placeimg.com/100/100/arch");
  width: 30px;
  height: 30px;
  background-size: 100%;
  border-radius: 50%;
  float: left;
}
.profile-name {
  display: block;
  float: left;
  padding-left: 10px;
  padding-top: 7px;
  font-size: 14px;
}
.post-header {
  height: 30px;
  padding: 10px;
}
.post-body {
  background-image: url("https://placeimg.com/640/480/animals");
  height: 450px;
  background-position: center;
  background-size: cover;
}
.post-content {
  padding-left: 15px;
  padding-right: 15px;
  font-size: 14px;
}
.date {
  font-size: 11px;
  color: grey;
  margin-top: -8px;
}
.upload-image {
  width: 100%;
  height: 450px;
  background: cornflowerblue;
  background-size: cover;
}
.filters {
  overflow-x: scroll;
  white-space: nowrap;
}
.filter-1 {
  width: 100px;
  height: 100px;
  background-color: cornflowerblue;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color: white;
  background-size: cover;
}
.filters::-webkit-scrollbar {
  height: 5px;
}
.filters::-webkit-scrollbar-track {
  background: #f1f1f1;
}
.filters::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
  background: #555;
}
.write-box {
  border: none;
  width: 90%;
  height: 100px;
  padding: 15px;
  margin: auto;
  display: block;
  outline: none;
}
</style>
