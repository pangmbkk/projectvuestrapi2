<template>
  <div class>
    <b-navbar toggleable="lg" type="light" variant="outline-dark">
      <b-navbar-brand href="http://localhost:3000/">Tutor Search</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="http://localhost:3000/">หน้าหลัก</b-nav-item>
          <b-nav-item href="http://localhost:3000/search">ค้นหาติวเตอร์</b-nav-item>
          <b-nav-item href="http://localhost:3000">วิชาเรียน</b-nav-item>
          <b-nav-item href="http://localhost:3000/about">เกี่ยวกับเว็บไซต์</b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown right  v-if="username">
                  <!-- Using 'button-content' slot -->
                  <template v-slot:button-content  v-if="username">
                    {{username}}
                  </template>
                 
                  <b-dropdown-item href="/editProfile">Profile</b-dropdown-item>
                  <b-dropdown-item href="/listPostmanage">การจัดการของติวเตอร์</b-dropdown-item>
                  <b-dropdown-item href="/studentmanage">การจัดการของนักเรียน</b-dropdown-item>
                </b-nav-item-dropdown>
          <div class="collapse navbar-collapse justify-content-end" right>
            <ul class="navbar-nav">
              <li v-if="username">
                <a href="#" class="nav-link" @click="logout">Logout</a>
              </li>
              <li v-if="!username">
                <router-link v-if="!username" tag="a" class="nav-link" to="/signin" exact>
                  <b-button variant="outline-primary">Signin</b-button>
                </router-link>
              </li>

              <li v-if="!username">
                <router-link v-if="!username" tag="a" class="nav-link" to="/signup" exact>
                  <b-button variant="primary">Signup</b-button>
                </router-link>
              </li>
            </ul>
          </div>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>

  <!-- <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <router-link tag="a" class="navbar-brand" to="/" exact>FIND TUTOR</router-link>
      <ul class="navbar-nav mr-auto mt-2 mt-lg-0">
        <li class="nav-item active">
          <a class="nav-link textcolor" href="http://localhost:3000/">
            หน้าหลัก
            <span class="sr-only">(current)</span>
          </a>
        </li>
        <li class="nav-item">
          <a class="nav-link text-dark" href="http://localhost:3000/search">ค้นหาติวเตอร์</a>
        </li>
        <li class="nav-item">
          <a class="nav-link text-dark" href="#">วิชาเรียน</a>
        </li>
        <li class="nav-item">
          <a class="nav-link text-dark" href="http://localhost:3000/about">เกี่ยวกับ</a>
        </li>
      </ul>
      <div class="collapse navbar-collapse justify-content-end">
        <ul class="navbar-nav">
          <li v-if="username">
            <a href="#" class="nav-link">Hello {{ username }}</a>
          </li>
          <li v-if="username">
            <a href="#" class="nav-link" @click="logout">Logout</a>
          </li>
          <li v-if="!username">
            <router-link v-if="!username" tag="a" class="nav-link" to="/signin" exact>
              <b-button variant="outline-primary">Signin</b-button>
            </router-link>
          </li>

          <li v-if="!username">
            <router-link v-if="!username" tag="a" class="nav-link" to="/signup" exact>
              <b-button variant="primary">Signup</b-button>
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>-->
</template>

<script>
import { mapMutations } from "vuex";

export default {
  computed: {
    username() {
      return this.$store.getters["auth/username"];
    }
  },
  methods: {
    ...mapMutations({
      logout: "auth/logout"
    })
  }
};
</script>

<style scoped>
b-nav-item {
  color: black;
}
.navbar {
  background-color: white !important ;
  display: flex;
  justify-content: space-between;
  background: inherit;
  box-sizing: border-box;
  height: 65px;

  margin: auto;

  box-shadow: 0 0 1px 1px rgba(20, 23, 28, 0.1),
    0 3px 1px 0 rgba(20, 23, 28, 0.1);
}
</style>
