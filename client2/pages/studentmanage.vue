<template>
  <div>
    <b-tabs content-class v-model="tabIndex" class="navb">
      <b-tab title="รายการที่ได้ร้องขอ" class="body" :title-link-class="linkClass(0)" active>
        <div class="container-fluid">
          <div class="container">
            <br />
            <div class="row">
              <div class="col-md">
                <br />
                <h2 class="text-center">รายการที่ได้ร้องขอ</h2>
                <br />
                <div class="router">
                  <Waitingpost :anpos=" postids" :waitingposts="waitingposts" />
                </div>
                <br />
              </div>
            </div>
          </div>
        </div>
      </b-tab>
      <b-tab title="รายการที่กำลังดำเนินการ" class="body" :title-link-class="linkClass(1)">
        <br />
        <p>I'm a disabled tab!</p>
      </b-tab>
      <b-tab title="รายการที่ติวเสร็จแล้ว" class="body" :title-link-class="linkClass(2)">
        <br />
        <p>I'm a disabled tab!</p>
      </b-tab>
      <b-tab title="รายการที่ยกเลิกแล้ว" class="body" :title-link-class="linkClass(3)">
        <br />
        <p>I'm a disabled tab!</p>
      </b-tab>
    </b-tabs>
  </div>
</template>
<style scoped>
.nav-item {
  color: white;
}
.body {
  background-color: white;
}
.navb {
  background-color: #29303b;
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
import Waitingpost from "../components/Waitingpost";
export default {
  components: {
    Waitingpost
  },
  computed: {
    username() {
      return this.$store.getters["auth/username"];
    }
  },
  data() {
    return {
      anpost: {}, //ตัววนลูปในตาราง annoucementpost
      postids: [],
      waitingposts: [],
      tabIndex: 0,
      announce: {
        id: "",
        name: "",
        description: "",
        detail: "",
        educationName: "",
        experienceName: "",
        provinceName: "",
        subjectName: "",
        tutorName: "",
        username: "",
        imageUrl: "",
        email: ""
      }
    };
  },
  async created() {
    axios
      .get(
        "http://localhost:1337/orders?status_in=waiting&studentusername_in=" +
          this.username
      )
      .then(response => {
        this.waitingposts = response.data;
        console.log("get postid success:" + this.waitingposts);
        console.log(this.waitingposts);
        for (let elm of this.waitingposts) {
          console.log(elm.postId);
          axios
            .get("http://localhost:1337/announcementposts?id=" + elm.postId)
            .then(res => {
              this.anpost = res.data;
              console.log("get Announcementposts by postid success");
              this.postids.push(...this.anpost);
              axios.put("http://localhost:1337/orders/" + elm.id, {
                announcement: res.data
              });
            });
        }
        console.log(this.postids);
      });
  },
  methods: {
    linkClass(idx) {
      if (this.tabIndex === idx) {
        return ["text-dark"];
      } else {
        return ["text-light"];
      }
    }
  }
};
</script >

