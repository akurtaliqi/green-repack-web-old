<template>
  <div>
    <base-info-card :title="title" :subtitle="subtitle" space="4" color="primary" />

    <form @submit.prevent="submit">
      <input v-model="email" type="email" />

      <input v-model="password" type="password" />

      <!--button type="submit">Log in</button-->

      <base-btn :color="!theme.isDark ? 'accent' : 'white'" outlined type="submit">
        Connexion
      </base-btn>
    </form>

    <!--base-text-field
      label="Email"
      v-model="email"
    />

    <base-text-field
      label="Password"
    /-->
  </div>
</template>

<script>
import { LOGINBUYERACTION } from "@/store/constants";
export default {
  name: "LoginBuyer",

  // Injected from the Vuetify Themeable mixin
  inject: ["theme"],

  props: {
    subtitle: String,
    title: {
      type: String,
      default: "VOUS ÊTES UN ACHETEUR",
    },
  },
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    /*async loginBuyer() {
      try {
        const response = await this.$http.post("/api/signup", this.register);
        console.log(response);
        const token = response.data.token;
        if (token) {
          localStorage.setItem("jwt", token);
          this.$router.push("/");
          console.log("Success", "Registration Was successful", "success");
        } else {
          console.log("Error", "Something Went Wrong", "Error");
        }
      } catch (err) {
        const error = err.response;
        if (error.status === 409) {
          console.log("Error", error.data.message, "error");
        } else {
          console.log("Error", error.data.err.message, "error");
        }
      }
    },*/
    async submit() {
      this.$store
        .dispatch(`Auth/${LOGINBUYERACTION}`, {
          email: this.email,
          password: this.password,
        })
        .then((res) => {
          if (res) {
            this.$router.push("/");
          }
        });
    },
  },
};
</script>
<style scoped>
input {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border-radius: 3px;
  background-color: white;
}
</style>
