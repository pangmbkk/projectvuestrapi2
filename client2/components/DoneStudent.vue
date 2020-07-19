<template>
  <div class="doneStudent">
    <div v-for="doneStudent in doneStudents" :key="doneStudent.id">
      <hr />
      <div class="row pointer">
        <div class="col-md-3">
          <nuxt-link :to="'detail/' + doneStudent.postId">
            <img class="card-img-left img-fluid" :src="doneStudent.announcement[0].imageUrl" alt />
          </nuxt-link>
        </div>

        <div class="col">
          <nuxt-link
            :to="'detail/' + doneStudent.postId"
            style="text-decoration: none;
  color: black;"
          >
            <h4 class="title">{{doneStudent.announcement[0].name}}</h4>

            <p>{{doneStudent.announcement[0].description}}</p>
          </nuxt-link>
        </div>

        <div class="col-2-auto">
          <nuxt-link
            :to="'detail/' + doneStudent.postId"
            style="text-decoration: none;
  color: black;"
          >
            <h4>ประกาศของ</h4>
            <p
              class="card-text"
            >{{ doneStudent.announcement[0].tutorName ||'No description provided' }}</p>
          </nuxt-link>
        </div>

        <div class="col-auto">
          <b-button squared variant="info">รีวิว</b-button>
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
  name: "DoneStudent",
  props: ["doneStudents", "id"]
};
</script>

