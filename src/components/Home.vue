<template>
  <div class="home">
    <img src="./../assets/Stalk-Forces_logo.jpg">

    <p
      style="color: #777777; font-size: 2.5vh; padding-top: 10px; padding-bottom: 10px;"
    >Explore what coders are solving!</p>
    <!-- Search Box -->
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
        <path class="border" d="M335.5,108.5h-280c-29.3,0-53-23.7-53-53v0c0-29.3,23.7-53,53-53h280"></path>
        <path class="border" d="M335.5,108.5h280c29.3,0,53-23.7,53-53v0c0-29.3-23.7-53-53-53h-280"></path>
      </svg>
      <div class="go-icon">
        <i class="fa fa-arrow-right"></i>
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
    },
    toggle: function() {
      this.showError = false;
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
.search-box {
  position: relative;
  width: 100%;
  max-width: 360px;
  height: 60px;
  border-radius: 120px;
  margin: 0 auto;
}
.search-icon,
.go-icon {
  position: absolute;
  top: 0;
  height: 60px;
  width: 86px;
  line-height: 61px;
  text-align: center;
}
.search-icon {
  left: 0;
  pointer-events: none;
  font-size: 1.22em;
  will-change: transform;
  transform: rotate(-45deg);
  -webkit-transform: rotate(-45deg);
  -moz-transform: rotate(-45deg);
  -o-transform: rotate(-45deg);
  transform-origin: center center;
  -webkit-transform-origin: center center;
  -moz-transform-origin: center center;
  -o-transform-origin: center center;
  transition: transform 400ms 220ms cubic-bezier(0.19, 1, 0.22, 1);
  -webkit-transition: transform 400ms 220ms cubic-bezier(0.19, 1, 0.22, 1);
  -moz-transition: transform 400ms 220ms cubic-bezier(0.19, 1, 0.22, 1);
  -o-transition: transform 400ms 220ms cubic-bezier(0.19, 1, 0.22, 1);
}
.si-rotate {
  transform: rotate(0deg);
  -webkit-transform: rotate(0deg);
  -moz-transform: rotate(0deg);
  -o-transform: rotate(0deg);
}
.go-icon {
  right: 0;
  pointer-events: none;
  font-size: 1.38em;
  will-change: opacity;
  cursor: default;
  opacity: 0;
  transform: rotate(45deg);
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  -o-transform: rotate(45deg);
  transition: opacity 190ms ease-out,
    transform 260ms cubic-bezier(0.19, 1, 0.22, 1);
  -webkit-transition: opacity 190ms ease-out,
    transform 260ms cubic-bezier(0.19, 1, 0.22, 1);
  -moz-transition: opacity 190ms ease-out,
    transform 260ms cubic-bezier(0.19, 1, 0.22, 1);
  -o-transition: opacity 190ms ease-out,
    transform 260ms cubic-bezier(0.19, 1, 0.22, 1);
}
.go-in {
  opacity: 1;
  pointer-events: all;
  cursor: pointer;
  transform: rotate(0);
  -webkit-transform: rotate(0);
  -moz-transform: rotate(0);
  -o-transform: rotate(0);
  transition: opacity 190ms ease-out,
    transform 260ms 20ms cubic-bezier(0.19, 1, 0.22, 1);
  -webkit-transition: opacity 190ms ease-out,
    transform 260ms 20ms cubic-bezier(0.19, 1, 0.22, 1);
  -moz-transition: opacity 190ms ease-out,
    transform 260ms 20ms cubic-bezier(0.19, 1, 0.22, 1);
  -o-transition: opacity 190ms ease-out,
    transform 260ms 20ms cubic-bezier(0.19, 1, 0.22, 1);
}
.search-border {
  display: block;
  width: 100%;
  max-width: 360px;
  height: 60px;
}
.border {
  fill: none;
  stroke: #575656;
  stroke-width: 5;
  stroke-miterlimit: 10;
}
.border {
  stroke-dasharray: 740;
  stroke-dashoffset: 0;
  transition: stroke-dashoffset 400ms cubic-bezier(0.6, 0.04, 0.735, 0.99);
  -webkit-transition: stroke-dashoffset 400ms
    cubic-bezier(0.6, 0.04, 0.735, 0.99);
  -moz-transition: stroke-dashoffset 400ms cubic-bezier(0.6, 0.04, 0.735, 0.99);
  -o-transition: stroke-dashoffset 400ms cubic-bezier(0.6, 0.04, 0.735, 0.99);
}
.border-searching .border {
  stroke-dasharray: 740;
  stroke-dashoffset: 459;
  transition: stroke-dashoffset 650ms cubic-bezier(0.755, 0.15, 0.205, 1);
  -webkit-transition: stroke-dashoffset 650ms
    cubic-bezier(0.755, 0.15, 0.205, 1);
  -moz-transition: stroke-dashoffset 650ms cubic-bezier(0.755, 0.15, 0.205, 1);
  -o-transition: stroke-dashoffset 650ms cubic-bezier(0.755, 0.15, 0.205, 1);
}
#search {
  font-family: "Montserrat Alternates", sans-serif;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 120px;
  border: none;
  background: rgba(255, 255, 255, 0);
  padding: 0 68px 0 68px;
  color: #0c0c0c;
  font-size: 1.32em;
  font-weight: 500;
  letter-spacing: -0.015em;
  outline: none;
}
#search::-webkit-input-placeholder {
  color: #888888;
}
#search::-moz-placeholder {
  color: #888888;
}
#search:-ms-input-placeholder {
  color: #888888;
}
#search:-moz-placeholder {
  color: #888888;
}
#search::-moz-selection {
  color: #888888;
  background: rgba(0, 0, 0, 0.25);
}
#search::selection {
  color: #ffffff;
  background: rgba(247, 243, 243, 0.25);
}
</style>
