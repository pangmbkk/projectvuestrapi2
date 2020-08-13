<template>
  <div class="doingStudent">
    <div v-for="doingStudent in doingStudents" :key="doingStudent.id">
      <hr />
      <div class="row pointer">
        <div class="col-md-3">
          <nuxt-link :to="'detail/' + doingStudent.postId">
            <img class="card-img-left img-fluid" :src="doingStudent.announcementpost.imageUrl" alt />
          </nuxt-link>
        </div>

        <div class="col">
          <nuxt-link
            :to="'detail/' + doingStudent.postId"
            style="text-decoration: none;
  color: black;"
          >
            <h4 class="title">{{doingStudent.announcementpost.name}}</h4>

            <p>{{doingStudent.announcementpost.description}}</p>
          </nuxt-link>
        </div>

        <div class="col-auto">
          <nuxt-link
            :to="'detail/' + doingStudent.postId"
            style="text-decoration: none;
  color: black;"
          >
            <h4>ประกาศ</h4>
            <p
              class="card-text"
            >{{ doingStudent.announcementpost.tutorName ||'No description provided' }}</p>
          </nuxt-link>
        </div>

        <div class="col-auto">
          <b-button squared variant="success" @click="showMsgBoxOne(doingStudent.id)">ติวเสร็จสิ้น</b-button>
        </div>
      </div>
    </div>
  </div>
</template>
<style>
</style>
<script>
import axios from "axios";
import Strapi from "strapi-sdk-javascript/build/main";
const apiUrl = process.env.API_URL || "http://localhost:1337";
const strapi = new Strapi(apiUrl);
export default {
  name: "DoingStudent",
  props: ["doingStudents", "id"],
  data() {
    return {
      boxOne: "",
    };
  },
  methods: {
    showMsgBoxOne(ids) {
      this.boxOne = "";
      this.$bvModal
        .msgBoxConfirm("ต้องยืนยันว่าการติวสิ้นสุดแล้ว?")
        .then((value) => {
          this.boxOne = value;
          if (value == true) {
            axios
              .put(apiUrl + "/orders/" + ids, {
                doingstatus: "true",
              })
              .then((res) => {
                console.log(res); //แก้ไข ข้อมูลในตาราง orders ตาม id ที่ได้กด มี สถานะ  doingstatus เป็น true คือ ทำการติวเสร็จแล้ว(done)
                this.$router.go();
              });
          }
        })
        .catch((err) => {
          // An error occurred
        });
    },
  },
};
</script>

