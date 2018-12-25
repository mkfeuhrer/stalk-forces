<template>
  <div class="home">
    <img src="./../assets/Stalk-Forces_logo.jpg">

    <p class="foot">Explore what coders are solving!</p>
    <!-- Search Box -->
    <SearchBox></SearchBox>
    <!-- Footer -->
    <Footer></Footer>
  </div>
</template>

<script>
import SearchBox from "./SearchBox";
import Footer from "./Footer";
export default {
  name: "Home",
  components: {
    SearchBox,
    Footer
  },
  data() {
    return {};
  }
};
</script>

<style scoped>
@import "./../assets/css/bootstrap.min.css";
.foot {
  color: #777777;
  font-size: 2.5vh;
  padding-top: 20px;
  padding-bottom: 10px;
}

.home {
  padding-top: 20px;
}
</style>
