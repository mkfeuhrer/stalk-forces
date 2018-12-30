<template>
  <div class="home">
    <img src="./../assets/Stalk-Forces_logo.jpg">

    <p
      style="color: #777777; font-size: 2.5vh; padding-top: 10px; padding-bottom: 10px;"
    >Explore what coders are solving!</p>
    <!-- Search Box -->
    <div class="row box">
      <div class="search-box">
        <div class="search-icon">
          <i class="fa fa-search search-icon"></i>
        </div>
        <form @submit.prevent="search()" class="search-form">
          <input
            type="text"
            v-model="username"
            name="username"
            placeholder="Codeforces Username"
            id="search"
            autocomplete="off"
          >
        </form>
        <svg
          class="search-border"
          version="1.1"
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
          xmlns:a="http://ns.adobe.com/AdobeSVGViewerExtensions/3.0/"
          x="0px"
          y="0px"
          viewBox="0 0 671 111"
          style="enable-background:new 0 0 671 111;"
          xml:space="preserve"
        >
          <path
            class="border"
            d="M335.5,108.5h-280c-29.3,0-53-23.7-53-53v0c0-29.3,23.7-53,53-53h280"
          ></path>
          <path
            class="border"
            d="M335.5,108.5h280c29.3,0,53-23.7,53-53v0c0-29.3-23.7-53-53-53h-280"
          ></path>
        </svg>
        <div class="go-icon">
          <i class="fa fa-arrow-right"></i>
        </div>
      </div>
    </div>

    <!-- Footer -->
    <Footer></Footer>
  </div>
</template>

<script>
import Footer from "./Footer";
window.select = require("./../assets/js/search_box.js");

export default {
  name: "Home",
  components: {
    Footer
  },
  data() {
    return {
      username: "",
      error: false
    };
  },
  methods: {
    search: function() {
      let user = this.username;
      if (user) {
        this.$router.push("/" + user);
      } else {
        this.showError = true;
      }
    }
  }
};
</script>

<style scoped>
@import "./../assets/css/bootstrap.min.css";

.home {
  margin-top: 100px;
  align-content: center;
}
.box {
  padding-bottom: 20px;
}
</style>
