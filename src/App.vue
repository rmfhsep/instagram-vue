<template>
  <div class="header">
    <ul class="header-button-left">
      <li @click="tab--">Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="tab === 1 || tab === 0" @click="tab++">Next</li>
      <li v-if="tab === 2" @click="post">Post</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>

  <ContainerComp
    :data="datas"
    :tab="tab"
    :imgUrl="imgUrl"
    @write="content = $event"
  />
  <button @click="getMoreData">More</button>

  <div class="footer">
    <ul class="footer-button-plus">
      <input
        @change="upload"
        accept="image/*"
        type="file"
        id="file"
        class="inputfile"
      />
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>
</template>

<script>
import ContainerComp from "./components/ContainerComp.vue";
import datas from "./data";
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      datas: datas,
      more: 0,
      tab: 0,
      imgUrl: "",
      content: "",
    };
  },
  components: {
    ContainerComp,
  },
  methods: {
    getMoreData() {
      axios
        .get(`https://codingapple1.github.io/vue/more${this.more}.json`)
        .then((res) => {
          const result = res.data;
          const newArr = [...this.datas];
          newArr.push(result);
          this.datas = newArr;
          this.more++;
        });
    },
    upload(e) {
      const imgFile = e.target.files[0];
      this.imgUrl = URL.createObjectURL(imgFile);
      this.tab = 1;
    },
    post() {
      const posts = {
        name: "Kim Hyun",
        userImage: "https://placeimg.com/100/100/arch",
        postImage: this.imgUrl,
        likes: 36,
        date: "May 15",
        liked: false,
        content: this.content,
        filter: "perpetua",
      };
      this.datas.unshift(posts);
      this.tab = 0;
    },
  },
  updated() {
    console.log(this.content);
  },
};
</script>

<style>
body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
</style>
