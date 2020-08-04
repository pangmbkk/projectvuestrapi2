<template>
  <div class="listpost">
    <hr />

    <div class="row pointer">
      <div class="col-md-3">
        <nuxt-link :to="'detail/' + id">
          <img class="card-img-left img-fluid" :src="listpost.imageUrl" alt />
        </nuxt-link>
      </div>

      <div class="col">
        <nuxt-link :to="'detail/' + id" style="text-decoration: none;
  color: black;">
          <h4 class="title">{{listpost.name}}</h4>

          <p>{{listpost.description}}</p>
        </nuxt-link>
      </div>

      <div class="col-2-auto">
        <nuxt-link :to="'detail/' + id" style="text-decoration: none;
  color: black;">
          <h4>ประกาศของ</h4>
          <p class="card-text">{{ listpost.tutorName ||'No description provided' }}</p>
        </nuxt-link>
      </div>

      <div class="col-auto">
        <NuxtLink :to="'/editpost/'+id">
          <button class="btn btn-primary">แก้ไข</button>
        </NuxtLink>

        <button class="btn btn-danger" @click="deletepost(id)">ลบ</button>
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
  name: "Listpost",
  props: ["listpost", "id"],
  data() {
    return {
      modalShow: false
    };
  },
  methods: {
    updatepost() {
      console.log("sssss");
    },
    async deletepost(ids) {
      axios
        .delete("http://localhost:1337/announcementposts/" + ids)
        .then(res => {
          console.log("deletepos success" + ids);
          console.log(res);
        });
      this.$router.go(0)
    }
  }
};
</script>


