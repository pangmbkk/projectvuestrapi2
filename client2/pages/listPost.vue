<template>
  <div class="container-fluid body">
    <div class="container">
      <br />
      <div class="row">
        <div class="col-md">
          <br />
          <h2 class="text-center">รายการโพสประกาศ</h2>
          <br />
          <div>
            <Listsearch
              class="router"
              v-for="listsearch in listsearchs"
              :key="listsearch.id"
              :id="listsearch.id"
              :listsearch="listsearch"
            />
          </div>
          <br />
          <div class="text-center">
              <b-link to="/form"><b-button squared variant="primary">เพิ่มโพสประกาศ</b-button></b-link>
            
          </div>
          <br />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Strapi from "strapi-sdk-javascript/build/main";
import axios from "axios";
const apiUrl = process.env.API_URL || "http://localhost:1337";
const strapi = new Strapi(apiUrl);
import Listsearch from "../components/Listsearch";
export default {
  components: {
    Listsearch
  },
    computed: {
    username() {
      return this.$store.getters["auth/username"];
    }
  },
  data() {
    return {
      listsearchs: []
    };
  },
  async created() {
    axios.get("http://localhost:1337/announcementposts?username="+this.username).then(response => {
      this.listsearchs = response.data;
      console.log("get Announcementposts success");
    });
  }
};
</script >

<style scoped>
.router {
  text-decoration: none;
  color: black;
}
.col-md {
  margin-left: 100px;
  margin-right: 100px;
}
</style>