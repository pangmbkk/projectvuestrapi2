<template>
  <div class="container-fluid">
    <div class="row titleo">
      <div class="col">
        <div class="row title align-items-center">
          <div class="col-2"></div>
          <h1 class="text-middle col">{{announcementposts.name}}</h1>
        </div>
        <div class="row description">
          <div class="col-2"></div>
          <p class="col">{{announcementposts.description}}</p>
        </div>
      </div>

      <b-button squared variant="danger" class="col-1 b" @click="pushpost()">เลือก</b-button>
      <b-modal ref="my-modal" hide-footer title="Using Component Methods">
        <div class="d-block text-center">
          <h3>Hello From My Modal!</h3>
        </div>
        <b-button class="mt-3" variant="outline-danger" block @click="hideModal">Close Me</b-button>
      </b-modal>

      <div class="col-1"></div>
    </div>

    <br />
    <div class="row">
      <!-- <div class="col-1"></div> -->
      <ul class="list-group col-7">
        <li class="list-group-item list-group-item-dark">เนื้อหาและข้อมูลประกอบ</li>
        <li class="list-group-item c1">
          <pre>
            {{detail}}
        </pre>
        </li>
      </ul>
      <ul class="list-group col-5">
        <li class="list-group-item list-group-item-dark">ข้อมูลส่วนตัวครูกวดวิชา</li>
        <li class="list-group-item c2">
          <b-media tag="li">
            <template v-slot:aside>
              <b-img blank blank-color="#bac" width="64" alt="placeholder"></b-img>
            </template>

            <h5 class="mt-3 mb-0">{{turorInformation.fname }} {{turorInformation.lname}}</h5>
          </b-media>
          <br />
          <form>
            <div class="form-group row">
              <div class="col-1"></div>
              <label for="staticEmail" class="col-sm-2-auto">วุฒิการศึกษา:</label>
              <div class="col-sm-9">
                <p>{{turorInformation.education}}</p>
              </div>
            </div>
            <div class="form-group row">
              <div class="col-1"></div>
              <label for="inputPassword" class="col-sm-2-auto">เบอร์โทรศัพท์</label>
              <div class="col-sm-9">
                <p>{{turorInformation.phone}}</p>
              </div>
            </div>
            <div class="form-group row">
              <div class="col-1"></div>
              <label for="inputPassword" class="col-sm-2-auto">E-mail:</label>
              <div class="col-sm-9">
                <p>{{turorInformation.email}}</p>
              </div>
            </div>
            <div class="form-group row">
              <div class="col-1"></div>
              <label for="inputPassword" class="col-sm-2-auto">ประสบการณ์:</label>
              <div class="col-sm-9">
                <p>{{announcementposts.experienceName}}</p>
              </div>
            </div>
            <div class="form-group row">
              <div class="col-1"></div>
              <label for="inputPassword" class="col-sm-2-auto">จังหวัด:</label>
              <div class="col-sm-9">
                <p>{{announcementposts.provinceName}}</p>
              </div>
            </div>
          </form>
        </li>
      </ul>
      <!-- <div class="col-1"></div> -->
    </div>
  </div>
</template>
<style scoped>
.b {
  margin-bottom: 2rem;
  margin-top: 2rem;
}
.titleo {
  background-color: #29303b;
}
.title {
  background-color: #29303b;
  color: aliceblue;
  height: 5rem;
}
.description {
  background-color: #29303b;
  color: aliceblue;
  height: 3rem;
}
.col-7 {
  padding-left: 2rem;
  padding-right: 1rem;
  padding-bottom: 2rem;
}
.col-5 {
  padding-left: 1rem;
  padding-right: 2rem;
  padding-bottom: 2rem;
}
.c1 {
  height: 100%;
}
.c2 {
  height: 90%;
}
</style>
<script>
import axios from "axios";
import Strapi from "strapi-sdk-javascript/build/main";
const apiUrl = process.env.API_URL || "http://localhost:1337";
const strapi = new Strapi(apiUrl);
export default {
  data() {
    return {
      announcementposts: [],
      detail: null,
      turorInformation: "",
      haveornot: false,
      postid: null,
      orderpostid: ""
    };
  },
  computed: {
    username() {
      return this.$store.getters["auth/username"];
    },
    studentuser() {
      return this.$store.getters["auth/tutoruser"];
    }
  },
  async created() {
    axios
      .get("http://localhost:1337/announcementposts/" + this.$route.params.id)   //get ตาราง announcementposts ที่มี id ตามที่กดมา
      .then(res => {
        this.announcementposts = res.data;      
        this.detail = res.data.detail;
        console.log("get announcementposts success");
        axios
          .get(
            "http://localhost:1337/users?username=" +
              this.announcementposts.username
          ) //get ตารางusers โดยใช้ username ให้ตรงกับ username ในตาราง announcementposts
          .then(Response => {
            this.turorInformation = Response.data[0];
            console.log(this.turorInformation);
            console.log(
              "get turorInformation user :" +
                this.turorInformation.username +
                " success"
            );
          });
      });
    if (this.username) {
      axios
        .get(
          "http://localhost:1337/orders?status_in=waiting&studentusername_in=" +
            this.username +
            "&postId_in=" +
            this.$route.params.id
        ) //ตราราง orders ที่มี status = waiting & studentusername this.username(คนที่login อยู่) & postId = id โพสประกาศ
        // .then(Response => {
        //   this.orderpostid = Response.data[0];
        //   this.postid = Response.data[0].postId; //เอาไปเช็ค เดิมๆมีอยู่ไหม
        //   console.log("postid:" + this.postid);
        // }
        // );
    }
  },
  methods: {
    pushpost() {
      if (this.postid == null) {
        axios
          .post("http://localhost:1337/orders", {
            tutorusername: this.turorInformation.username,
            studentusername: this.studentuser.username,
            status: "waiting",
            postid: this.$route.params.id,
            announcementpost: this.announcementposts
          })
          .then(res => {
            console.log(res.data);
            this.$router.push("/studentmanage");
          });
      } else {
        // alert("คุณได้เลือกรายการนี้แล้ว")
        this.$refs["my-modal"].show();
      }
    },
    hideModal() {
      this.$refs["my-modal"].hide();
      this.$router.push("/studentmanage");
    }
  }
};
</script>


