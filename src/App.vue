<template>
  <v-fade-transition mode="out-in">
    <router-view />
  </v-fade-transition>
</template>

<script>
import { LOGINUSERFROMLOCALSTORAGE } from "@/store/constants";
export default {
  name: "App",
  metaInfo: {
    title: "App",
    titleTemplate: "%s | Zero Pro",
    htmlAttrs: { lang: "en" },
    meta: [
      { charset: "utf-8" },
      { name: "viewport", content: "width=device-width, initial-scale=1" },
    ],
  },
  mounted() {
    this.LoginFromCache();
  },
  methods: {
    LoginFromCache() {
      this.$store.dispatch(
        `Auth/${LOGINUSERFROMLOCALSTORAGE}`,
        JSON.parse(localStorage.getItem("token"))
      );
    },
  },
};
</script>

<style lang="sass">
.extra-padding
  padding-bottom: 96px !important
  padding-top: 96px !important

  @media screen and (max-width: 959px)
    padding-top: 48px !important
    padding-bottom: 48px !important
</style>
