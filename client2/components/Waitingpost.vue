<template>
  <div class="waitingpost">
    <div v-for="waitingpost in waitingposts" :key="waitingpost.id"> 
      <hr />
      <!-- <div>{{waitingpost.id}}</div><div>{{waitingpost.postId}}</div> -->
      <div class="row pointer">
        <div class="col-md-3">
          <nuxt-link :to="'detail/' + waitingpost.postId">
            <img class="card-img-left img-fluid" :src="waitingpost.announcement[0].imageUrl"  alt />
          </nuxt-link>
        </div>

        <div class="col">
          <nuxt-link :to="'detail/' + waitingpost.postId" style="text-decoration: none;
  color: black;">
            <h4 class="title">{{waitingpost.announcement[0].name}}</h4>

            <p>{{anpos.description}}</p>
          </nuxt-link>
        </div>

        <div class="col-auto">
          <nuxt-link :to="'detail/' + waitingpost.postId" style="text-decoration: none;
  color: black;">
            <h4>ประกาศของ</h4>
            <p class="card-text">{{ waitingpost.announcement[0].tutorName ||'No description provided' }}</p>
          </nuxt-link>
        </div>

        <div class="col-auto">
          <b-button squared variant="danger"  @click="deleteorder(waitingpost.id)">ลบ</b-button>
          
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
</style>
<script>
import axios from "axios";
import Strapi from "strapi-sdk-javascript/build/main";
const apiUrl = process.env.API_URL || "http://localhost:1337";
const strapi = new Strapi(apiUrl);
export default {
  name: "Waitingpost",
  props: ["waitingposts", "postid", "id", "anpos"],
  data() {
    return {
      modalShow: false
    };
  },
  methods: {
    updatepost() {
      console.log("sssss");
    },
    async deleteorder(ids) {
      axios.delete(apiUrl+"/orders/" + ids).then(res => {
        console.log("deletepos success" + ids);
        console.log(res);
      });
      location.reload();
    }
  }
};
</script>


