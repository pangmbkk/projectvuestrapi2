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
                <h2 class="text-center">รายการที่ได้ร้องขอ ( นักเรียน )</h2>
                <br />
                <div class="router">
                  <Waitingpost  :waitingposts="waitingposts" />
                </div>
              </div>
            </div>
          </div>
        </div>
      </b-tab>
      <b-tab title="รายการที่กำลังดำเนินการ" class="body" :title-link-class="linkClass(1)">
        <div class="container-fluid">
          <div class="container">
            <br />
            <div class="row">
              <div class="col-md">
                <br />
                <h2 class="text-center">รายการที่กำลังดำเนินการ ( นักเรียน )</h2>
                <br />
                <div class="router">
                  <DoingStudent :doingStudents="doingStudents" />
                </div>
              </div>
            </div>
          </div>
        </div>
      </b-tab>
      <b-tab title="รายการที่ติวเสร็จแล้ว" class="body" :title-link-class="linkClass(2)">
        <div class="container-fluid">
          <div class="container">
            <br />
            <div class="row">
              <div class="col-md">
                <br />
                <h2 class="text-center">รายการที่ติวเสร็จแล้ว ( นักเรียน )</h2>
                <br />
                <div class="router">
                  <DoneStudent :doneStudents="doneStudents" />
                </div>
              </div>
            </div>
          </div>
        </div>
      </b-tab>
      <b-tab title="รายการที่ยกเลิกแล้ว" class="body" :title-link-class="linkClass(3)">
        <div class="container-fluid">
          <div class="container">
            <br />
            <div class="row">
              <div class="col-md">
                <br />
                <h2 class="text-center">รายการที่ยกเลิกแล้ว ( นักเรียน )</h2>
                <br />
                <div class="router">
                  <CancleStudent :cancleStudents="cancleStudents" />
                </div>
              </div>
            </div>
          </div>
        </div>
      </b-tab>
    </b-tabs>
  </div>
</template>
<style scoped>
.col-md {
  margin-left: 100px;
  margin-right: 100px;
}
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
</style>
<script>
import Strapi from "strapi-sdk-javascript/build/main";
import axios from "axios";
const apiUrl = process.env.API_URL || "http://localhost:1337";
const strapi = new Strapi(apiUrl);
import Waitingpost from "../components/Waitingpost";
import DoingStudent from "../components/DoingStudent";
import CancleStudent from "../components/CancleStudent";
import DoneStudent from "../components/DoneStudent"
export default {
  components: {
    Waitingpost,
    DoingStudent,
    CancleStudent,
    DoneStudent
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
      doingStudents: [],
      doneStudents: [],
      cancleStudents: [],
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
        this.waitingposts = response.data; //order
        console.log("get orders รายหารร้องขอวนักเรียน success:" );
        console.log(this.waitingposts);
        // for (let elm of this.waitingposts) {
        //   console.log(elm.postId);
        //   axios
        //     .get("http://localhost:1337/announcementposts?id=" + elm.postId)
        //     .then(res => {
        //       this.anpost = res.data;
        //       console.log("get Announcementposts by postid success");
        //       this.postids.push(...this.anpost);
        //       axios.put("http://localhost:1337/orders/" + elm.id, {
        //         announcementt: res.data //โพสประกาศของ orders
        //       });
        //     });
        // }
        // console.log(this.postids);
      });
    axios
      .get(
        "http://localhost:1337/orders?status_in=accept&studentusername_in=" +
          this.username +
          "&doingstatus_in=false"
      )
      .then(response => {
        this.doingStudents = response.data; // orderที่มีสถานะกำลีงดำเนินการของนักเรียน แต่ยังไม่เสร็จ (ให้ยังไม่เสร็จเป็น fale เสร็จเป้ข true)
        console.log("get ordersที่ถูกยกเลิก");
        console.log(this.doingStudents);
      });
    axios
      .get(
        "http://localhost:1337/orders?status_in=accept&studentusername_in=" +
          this.username +
          "&doingstatus_in=true"
      )
      .then(response => {
        this.doneStudents = response.data; // orderที่มีสถานะทำเสร็จแล้วของนักเรียน (ให้ยังไม่เสร็จเป็น fale เสร็จเป้ข true)
        console.log("get ordersดำเนินการเสร็จแล้ว");
        console.log(this.doneStudents);
      });
    axios
      .get(
        "http://localhost:1337/orders?status_in=cancle&studentusername_in=" +
          this.username
      )
      .then(response => {
        this.cancleStudents = response.data; // orderที่มีสถานะถูกยกเลิก ของนักเรียน
        console.log("get ordersที่ถูกยกเลิก");
        console.log(this.cancleStudents);
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

