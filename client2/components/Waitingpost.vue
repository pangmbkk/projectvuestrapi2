<template>
  <div class="waitingpost">
    <hr />

    <div class="row pointer">
      <div class="col-md-3">
        <nuxt-link :to="'detail/' + id">
          <img class="card-img-left img-fluid" :src="anpos.imageUrl" alt />
        </nuxt-link>
      </div>

      <div class="col">
        <nuxt-link :to="'detail/' + id" style="text-decoration: none;
  color: black;">
          <h4 class="title">{{anpos.name}}</h4>

          <p>{{anpos.description}}</p>
        </nuxt-link>
      </div>

      <div class="col-auto">
        <nuxt-link :to="'detail/' + id" style="text-decoration: none;
  color: black;">
          <h4>ประกาศของ</h4>
          <p class="card-text">{{ anpos.tutorName ||'No description provided' }}</p>
        </nuxt-link>
      </div>

      <div class="col-auto">
        <button class="btn btn-danger" >ลบ</button>
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
  props: ["waitingpost","postid", "id","anpos"],
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
      axios
        .delete("http://localhost:1337/orders/" + ids)
        .then(res => {
          console.log("deletepos success" + ids);
          console.log(res);
        });
      location.reload();
    }
  }
};
</script>


