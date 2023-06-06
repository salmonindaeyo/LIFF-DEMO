<template>
  <div>
    <lottie-animation path="/dist/assets/test.json" />
    <h1>create-liff-app</h1>
    <p v-if="message">{{ message }}</p>
    <p v-if="error">
      <code>{{ error }}</code>
    </p>
    <p v-if="os">
      <code>os : {{ os }}</code>
    </p>
    <p v-if="Language">
      <code>Language : {{ Language }}</code>
    </p>
    <p v-if="getVersion">
      <code>getVersion : {{ getVersion }}</code>
    </p>
    <p v-if="isInClient">
      <code>isInClient : {{ isInClient }}</code>
    </p>
    <p v-if="isLoggedIn">
      <code>isLoggedIn : {{ isLoggedIn }}</code>
    </p>
    <p v-if="getLineVersion">
      <code>getLineVersion : {{ getLineVersion }}</code>
    </p>
    <p v-if="profile">
      <code>profile : {{ profile }}</code>
    </p>
  </div>
</template>

<script>
import liff from "@line/liff";
import LottieAnimation from "lottie-vuejs/src/LottieAnimation.vue"; // import lottie-vuejs

export default {
  components: {
    LottieAnimation
  },
  data() {
    return {
      message: "",
      error: "",
      os: "",
      Language: "",
      getVersion: "",
      isInClient: "",
      isLoggedIn: "",
      getLineVersion: "",
      profile: ""
    };
  },
  mounted() {
    liff
      .init({
        liffId: import.meta.env.VITE_LIFF_ID
      })
      .then(() => {
        this.message = "LIFF init succeeded.";
        this.os = liff.getOS();
        this.getLanguage = liff.getLanguage();
        this.getLineVersion = liff.getVersion();
        this.isInClient = liff.isInClient();
        this.isLoggedIn = liff.isLoggedIn();
        this.getLineVersion = liff.getLineVersion();
        this.profile = liff.getProfile();
      })
      .catch(e => {
        this.message = "LIFF init failed.";
        this.error = `${e}`;
      });
  },
  methods: {
    getEnvironment() {
      console.log(liff.getOs());
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
