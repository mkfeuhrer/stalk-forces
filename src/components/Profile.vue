<template>
  <div class="profile">
    <div class="row">
      <div class="logo col-sm">
        <router-link to="/">
          <img style="width:18%;" src="./../assets/Stalk-Forces_logo.jpg">
        </router-link>
      </div>
      <div class="box col-sm">
        <!-- <div class="search-box">
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
        </div>-->
      </div>
      <div class="col-sm"></div>
    </div>

    <!-- Search Box -->
    <div id="spinner" v-if="loading"></div>

    <div v-if="!error&&!loading" class="main">
      <section class="userdata">
        <div class="row">
          <div class="col-md-4">
            <div class="dp">
              <img style="width:60%;" :src="profile.titlePhoto">
              <div class="details">
                <div style="font-size:3.5vh;">{{profile.firstName}} {{profile.lastName}}</div>
                <div style="margin-top: 10px;font-size:3vh;">{{profile.handle}}</div>
                <div style="margin-top: 10px;font-size:3vh;">
                  <span>
                    <img src="./../assets/location.png">
                  </span>
                  <span>{{profile.city}} , {{profile.country}}</span>
                </div>
              </div>
            </div>
          </div>
          <div class="col-md-2"></div>
          <div class="col-md-6">
            <!-- <p>Rating = {{profile.rating}}</p>
            <p>Max Rating = {{profile.maxRating}}</p>
            <p>Email = {{profile.email}}</p>
            <p>Rank = {{profile.rank}}</p>-->
          </div>
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
window.select = require("./../assets/js/search_box.js");

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
    },
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
@import "./../assets//css/search_box.css";

.message {
  padding-top: 20px;
  padding-bottom: 60px;
}

.error {
  margin-top: 15vh;
}

.logo {
  text-align: left;
  padding-top: 1vh;
  padding-left: 6vh;
}

.box {
  padding-top: 1.5vh;
}

.dp {
  padding: 5vh;
}

.details {
  padding-top: 3vh;
}
#spinner {
  display: inline-block;
  width: 100px;
  height: 100px;
  border: 3px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  border-top-color: rgb(46, 46, 46);
  animation: spin 1s ease-in-out infinite;
  -webkit-animation: spin 1s ease-in-out infinite;
}

@keyframes spin {
  to {
    -webkit-transform: rotate(360deg);
  }
}
@-webkit-keyframes spin {
  to {
    -webkit-transform: rotate(360deg);
  }
}
</style>
