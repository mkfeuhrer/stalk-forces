<template>
  <div class="foot">
    <!-- Don't judge me over some inline - thats just lazy me! -->
    <footer>
      Built with
      <span style="color:red">&#10084;</span> by
      <a style="color:#555555;" href="https://github.com/mkfeuhrer" target="blank">mkfeuhrer</a>
    </footer>
  </div>
</template>

<script>
export default {
  name: "Footer",
  data() {
    return {};
  }
};
</script>

<style>
footer {
  height: auto;
  width: 100%;
  bottom: 0;
  left: 0;
  z-index: -1;
  background: #ffffff;
}

a {
  color: rgb(0, 0, 0);
  text-decoration: none;
  display: inline-block;
  position: relative;
}
a:after {
  background: none repeat scroll 0 0 transparent;
  bottom: 0;
  content: "";
  display: block;
  height: 2px;
  left: 50%;
  background: rgb(0, 0, 0);
  transition: width 0.3s ease 0s, left 0.3s ease 0s;
  width: 0;
}
a:hover:after {
  width: 100%;
  left: 0;
}

.foot {
  color: #777777;
  font-size: 2.5vh;
  padding-top: 40px;
  padding-bottom: 10px;
}
</style>
