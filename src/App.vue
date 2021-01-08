<template>
  <div id="app">
    <div class="container-fluid">
      <div class="position-fixed image-card">
        <div class="text-center">
          <img src="./assets/cover.png" class="mt-5 img-fluid" />
        </div>
      </div>
      <h2 class="mt-3 position-fixed user-name text-nowrap">{{ user.name }}</h2>
      <div class="row">
        <div class="d-none d-md-block col-md-6 vh-100 bg-pink-600"></div>
        <div class="d-none d-md-block col-md-6 vh-100 bg-pink-700"></div>
      </div>
      <div>
        <ul class="nav-links">
          <li><a href="#">Home</a></li>
          <li><a href="#">About</a></li>
          <li class="nav-img">
            <img
              src="./assets/img-2.jpg"
              class="img-fluid rounded-circle"
              width="65"
              height="5"
              style="height: 65px;"
            />
          </li>
          <li><a href="#">Gallery</a></li>
          <li><a href="#">Contact</a></li>
        </ul>
      </div>
      <div class="icon-bar">
        <a :href="user.social_media.instagram" class="linkedin"
          ><i class="fa fa-instagram"></i
        ></a>
        <a :href="user.social_media.twitter" class="twitter"
          ><i class="fa fa-twitter"></i
        ></a>
        <a :href="user.social_media.snapchat" class="facebook"
          ><i class="fa fa-snapchat"></i
        ></a>
        <a :href="user.social_media.email" class="youtube"
          ><i class="fa fa-envelope"></i
        ></a>
      </div>
    </div>
  </div>
</template>
<script>
import "../src/assets/style.css";
export default {
  name: "App",
  data() {
    return {
      user: {
        name: "AQUILA AVEIONEN",
        social_media: {
          twitter: null,
          instagram: null,
          snapchat: null,
          email: null,
        },
      },
    };
  },
  methods: {
    async loadData() {
      await fetch("https://hirng-x2021.glitch.me/api")
        .then((res) => {
          if (res.status === 200) {
            return res.json();
          } else {
            alert("API ERROR ⚠ - API RETURNED STATUS CODE " + res.status);
            return
          }
        })
        .then((data) => {
          this.user.name = data.name;
          this.user.social_media.twitter = `https://twitter.com/${data.social_media.twitter}`;
          this.user.social_media.instagram = `https://instagram.com/${data.social_media.instagram}`;
          this.user.social_media.snapchat = `https://snapchat.com/${data.social_media.snapchat}`;
          this.user.social_media.email = `mailto:${data.social_media.email}`;
        });
    },
  },
  mounted() {
    this.loadData();
  },
};
</script>
