<template>
  <div class="container">
    <div>{{tutoruser}}</div>
    <h2 class="text-center">แก้ไขโปรไฟล์</h2>
    <form >
      <div class="form-group">
        <label for="exampleInputEmail1">Email address</label>
        <input
          type="email"
          class="form-control"
          id="exampleInputEmail1"
          aria-describedby="emailHelp"
          v-model="email"
        />
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1">ชื่อขนามสกุล</label>
        <input type="username" class="form-control" id="username" v-model="username" />
      </div>
      <div class="form-group">
        <label for="exampleInputPassword1">Password</label>
        <input type="password" class="form-control" id="exampleInputPassword1" v-model="password" />
      </div>

      <button type="submit" class="btn btn-primary" v-on:click.stop.prevent="onEdit()">แก้ไข</button>
    </form>
  </div>
</template>

<script>
import Strapi from "strapi-sdk-javascript/build/main";
import axios from "axios";
const apiUrl = process.env.API_URL || "http://localhost:1337";
const strapi = new Strapi(apiUrl);
export default {
  computed: {
    tutoruser() {
      return this.$store.getters["auth/tutoruser"];
    }
  },
  data() {
    return {
      username: "",
      email: "",
      password: ""
    };
  },
  async created() {
    this.email = this.tutoruser.email;
    this.username = this.tutoruser.username;
  },
  methodes: {
    onEdit() {
      axios
        .put("http://localhost:1337/user?username=" + this.tutoruser.username, {
          username: this.username,
          password: this.password,
          email: this.email
        })
        .then(response => {
          console.log(response);
        });
    }
  }
};
</script>

<style>
</style>