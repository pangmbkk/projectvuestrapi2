<template>
  <div class="cancleStudent">
    <div v-for="cancleStudent in cancleStudents" :key="cancleStudent.id">
      <hr />
      <div class="row pointer">
        <div class="col-md-3">
          <nuxt-link :to="'detail/' + cancleStudent.postId">
            <img class="card-img-left img-fluid" :src="cancleStudent.announcementpost.imageUrl" alt />
          </nuxt-link>
        </div>

        <div class="col">
          <nuxt-link
            :to="'detail/' + cancleStudent.postId"
            style="text-decoration: none;
  color: black;"
          >
            <h4 class="title">{{cancleStudent.announcementpost.name}}</h4>

            <p>{{cancleStudent.announcementpost.description}}</p>
          </nuxt-link>
        </div>

        <div class="col-2-auto">
          <nuxt-link
            :to="'detail/' + cancleStudent.postId"
            style="text-decoration: none;
  color: black;"
          >
            <h4>ประกาศของ</h4>
            <p
              class="card-text"
            >{{ cancleStudent.announcementpost.tutorName ||'No description provided' }}</p>
          </nuxt-link>
        </div>

        <div class="col-auto">
          <button class="btn btn-success">ตอบรับ</button>
          <button class="btn btn-danger">ยกเลิก</button>
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
  name: "CancleStudent",
  props: ["cancleStudents", "id"]
};
</script>

