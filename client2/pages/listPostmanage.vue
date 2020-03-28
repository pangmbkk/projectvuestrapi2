<template>
  <div>
    <b-tabs content-class="" v-model="tabIndex"  class="navb" >
        <b-tab title="รายการโพสประกาศ"  class="body" :title-link-class="linkClass(0)"  active>
        <div class="container-fluid ">
          <div class="container">
            <br />
            <div class="row">
              <div class="col-md">
                <br />
                <h2 class="text-center">รายการโพสประกาศ</h2>
                <br />
                <div class="router">
                  <Listpost
                    class="router"
                    v-for="listpost in listposts"
                    :key="listpost.id"
                    :id="listpost.id"
                    :listpost="listpost"
                  />
                </div>
                <br />
                <div class="text-center">
                  <b-link to="/form">
                    <b-button squared variant="primary">เพิ่มโพสประกาศ</b-button>
                  </b-link>
                </div>
                <br />
              </div>
            </div>
          </div>
        </div>
      </b-tab>
      <b-tab title="รายการที่รอการตอบรับ" class="body" :title-link-class="linkClass(1)">
        <br>
        <p>I'm a disabled tab!</p>
      </b-tab>
      <b-tab title="รายการที่กำลังดำเนินการ" class="body" :title-link-class="linkClass(2)">
        <br>
        <p>I'm the second tab</p>
      </b-tab>
      <b-tab title="รายการที่ติวเสร็จแล้ว" class="body" :title-link-class="linkClass(3)">
        <br>
        <p>I'm a disabled tab!</p>
      </b-tab>
      <b-tab title="รายการที่ยกเลิกแล้ว" class="body" :title-link-class="linkClass(4)">
        <br>
        <p>I'm a disabled tab!</p>
      </b-tab>
    </b-tabs>
  </div>
</template>
<style scoped>
.nav-item{
  color:white;
}
.body{
  background-color: white;
  
}
.navb{
  background-color: #29303B;
}
.router {
  text-decoration: none;
  color: black;
}
.col-md {
  margin-left: 100px;
  margin-right: 100px;
}
</style>
<script>
import Strapi from "strapi-sdk-javascript/build/main";
import axios from "axios";
const apiUrl = process.env.API_URL || "http://localhost:1337";
const strapi = new Strapi(apiUrl);
import Listpost from "../components/Listpost";
export default {
  components: {
    Listpost
  },
  computed: {
    username() {
      return this.$store.getters["auth/username"];
    }
  },
  data() {
    return {
      listposts: [],
      tabIndex: 0
 
    };
  },
  async created() {
    axios
      .get("http://localhost:1337/announcementposts?username=" + this.username)
      .then(response => {
        this.listposts = response.data;
        console.log("get Announcementposts success");
      });
  },
  methods:{
      linkClass(idx) {
        if (this.tabIndex === idx) {
          return [ 'text-dark']
        } else {
          return [ 'text-light']
        }
      }
  }
};
</script >

