<template>
  <div class="profile">
    <!-- <div class="logo">
      <router-link to="/">
        <img src="./../assets/Stalk-Forces_logo.jpg">
      </router-link>
    </div>-->
    <div class="spinner" v-if="loading"></div>

    <div v-if="!error&&!loading" class="main">
      <section class="userdata">
        <div class="dp">
          <img :src="profile.titlePhoto">
        </div>
        <div class="name">
          <p>{{profile.handle}}</p>
          <p>{{profile.firstName}} {{profile.lastName}}</p>
          <p>{{profile.city}} , {{profile.country}}</p>
          <p>Rating = {{profile.rating}}</p>
          <p>Max Rating = {{profile.maxRating}}</p>
          <p>Email = {{profile.email}}</p>
          <p>Rank = {{profile.rank}}</p>
        </div>
      </section>
      <Footer></Footer>
    </div>

    <div v-if="error&&!loading" class="error">
      <div class="errorimage">
        <img src="../assets/error.jpg">
      </div>
      <div class="message">
        <h2>Username not found.</h2>
        <h3>Has this user started coding yet ?.</h3>
      </div>
      <Footer></Footer>
    </div>
  </div>
</template>

<script>
import Footer from "./Footer";
import axios from "axios";

export default {
  name: "Profile",
  components: {
    Footer
  },
  data() {
    return {
      profile: [],
      submissions: [],
      username: "",
      blog: [],
      error: false,
      loading: true
    };
  },
  mounted: function() {
    // username from home page
    let user = this.$route.params.userId;
    this.username = user;
    // make request to codeforces
    this.makeRequest(user);
    window.onpopstate = event => {
      this.$router.push("/");
    };
  },
  computed: {
    getRatings: function() {}
  },
  methods: {
    makeRequest: function(username) {
      this.loading = true;
      this.error = false;
      axios
        .all([
          axios.get("https://codeforces.com/api/user.info?handles=" + username),
          axios.get(
            "https://codeforces.com/api/user.status?handle=" +
              username +
              "&from=1&count=10"
          ),
          axios.get(
            "https://codeforces.com/api/user.blogEntries?handle=" + username
          )
        ])
        .then(
          axios.spread((profile, submissions, blog) => {
            this.loading = false;
            this.profile = profile.data.result[0];
            this.submissions = submissions.data.result;
            this.blog = blog;
          })
        )
        .catch(err => {
          this.loading = false;
          console.log(err);
          this.error = true;
        });
    }
  }
};
</script>

<style scoped>
@import "./../assets/css/bootstrap.min.css";

.message {
  padding-top: 20px;
  padding-bottom: 60px;
}

.error {
  margin-top: 15vh;
}
</style>
