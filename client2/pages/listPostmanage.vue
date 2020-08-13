<template>
  <div>
    <b-tabs content-class v-model="tabIndex" class="navb">
      <b-tab title="รายการโพสประกาศ" class="body" :title-link-class="linkClass(0)" active>
        <div class="container-fluid">
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
                  <nuxt-link :to="'form'" style="text-decoration: none;
  color: white;">
                    <b-button squared variant="info">เพิ่มโพสประกาศ</b-button>
                  </nuxt-link>
                </div>
                <br />
              </div>
            </div>
          </div>
        </div>
      </b-tab>
      <b-tab title="รายการที่รอการตอบรับ" class="body" :title-link-class="linkClass(1)">
        <div class="container-fluid">
          <div class="container">
            <br />
            <div class="row">
              <div class="col-md">
                <br />
                <h2 class="text-center">รายการทีรอการตอบรับ</h2>
                <br />
                <div class="router">
                  <Tutorwaiting :tutorwaitings="tutorwaitings" />
                </div>
                <br />
              </div>
            </div>
          </div>
        </div>
      </b-tab>
      <b-tab title="รายการที่กำลังดำเนินการ" class="body" :title-link-class="linkClass(2)">
        <div class="container-fluid">
          <div class="container">
            <br />
            <div class="row">
              <div class="col-md">
                <br />
                <h2 class="text-center">รายการทีกำลังดำเนินการ</h2>
                <br />
                <div class="router">
                  <DoingTutor :doingTutors="doingTutors" />
                </div>
                <br />
              </div>
            </div>
          </div>
        </div>
      </b-tab>
      <b-tab title="รายการที่ติวเสร็จแล้ว" class="body" :title-link-class="linkClass(3)">
        <div class="container-fluid">
          <div class="container">
            <br />
            <div class="row">
              <div class="col-md">
                <br />
                <h2 class="text-center">รายการทีติวเสร็จแล้ว</h2>
                <br />
                <div class="router">
                  <DoneTutor :doneTutors="doneTutors" />
                </div>
                <br />
              </div>
            </div>
          </div>
        </div>
      </b-tab>
      <b-tab title="รายการที่ยกเลิกแล้ว" class="body" :title-link-class="linkClass(4)">
        <br />
        <p>I'm a disabled tab!</p>
      </b-tab>
    </b-tabs>
  </div>
</template>
<style scoped>
/* b-button{
  color: white;
} */
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
import Tutorwaiting from "../components/Tutorwaiting";
import DoingTutor from "../components/DoingTutor";
import DoneTutor from "../components/DoneTutor"
import CancleTutor from "../components/CancleTutor"
export default {
  components: {
    Listpost,
    Tutorwaiting,
    DoingTutor,
    DoneTutor,
    CancleTutor
  },
  computed: {
    username() {
      return this.$store.getters["auth/username"];
    }
  },
  data() {
    return {
      listposts: [],
      tutorwaitings: [],
      doingTutors: [],
      doneTutors: [],
      cancleTutors:[],
      tabIndex: 0
    };
  },
  async created() {
    axios
      .get("http://localhost:1337/announcementposts?username=" + this.username)
      .then(response => {
        this.listposts = response.data; // โพสประกาศที่ ติวเตอร์สร้างขึ้น
        console.log("get Announcementposts success");
      });
    axios
      .get(
        "http://localhost:1337/orders?status_in=waiting&tutorusername_in=" +
          this.username
      )
      .then(response => {
        this.tutorwaitings = response.data; // order tabรอการตอบรับ
        console.log("get ordersรอการตอบรับ");
        console.log(this.tutorwaitings);
      });
    axios
      .get(
        "http://localhost:1337/orders?status_in=accept&tutorusername_in=" +
          this.username +
          "&doingstatus_in=false"
      )
      .then(response => {
        this.doingTutors = response.data; // orderที่มีสถานะกำลังทำแต่ยังไม่เสร็จ (ให้ยังไม่เสร็จเป็น fale เสร็จเป้ข true)
        console.log("get ordersกำลังดำเนินการ");
        console.log(this.doingTutors);
      });
    axios
      .get(
        "http://localhost:1337/orders?status_in=accept&tutorusername_in=" +
          this.username +
          "&doingstatus_in=true"
      )
      .then(response => {
        this.doneTutors = response.data; // orderที่มีสถานะทำเสร็จแล้ว (ให้ยังไม่เสร็จเป็น fale เสร็จเป้ข true)
        console.log("get ordersดำเนินการเสร็จแล้ว");
        console.log(this.doneTutors);
      });
      axios
      .get(
        "http://localhost:1337/orders?status_in=cancle&tutorusername_in=" +
          this.username
      )
      .then(response => {
        this.cancleTutors = response.data; // orderที่มีสถานะถูกยกเลิก
        console.log("get ordersที่ถูกยกเลิก");
        console.log(this.cancleTutors);
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

