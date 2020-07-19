<template>
  <div class="cancleTutor">
    <div v-for="cancleTutor in cancleTutors" :key="cancleTutor.id">
      <hr />
      <div class="row pointer">
        <div class="col-md-3">
          <nuxt-link :to="'detail/' + cancleTutor.postId">
            <img class="card-img-left img-fluid" :src="cancleTutor.announcement[0].imageUrl" alt />
          </nuxt-link>
        </div>

        <div class="col">
          <nuxt-link
            :to="'detail/' + cancleTutor.postId"
            style="text-decoration: none;
  color: black;"
          >
            <h4 class="title">{{cancleTutor.announcement[0].name}}</h4>

            <p>{{cancleTutor.announcement[0].description}}</p>
          </nuxt-link>
        </div>

        <div class="col-2-auto">
          <nuxt-link
            :to="'detail/' + cancleTutor.postId"
            style="text-decoration: none;
  color: black;"
          >
            <h4>ประกาศของ</h4>
            <p
              class="card-text"
            >{{ cancleTutor.announcement[0].tutorName ||'No description provided' }}</p>
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
  name: "CancleTutor",
  props: ["cancleTutors", "id"]
};
</script>

