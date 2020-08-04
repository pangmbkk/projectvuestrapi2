<template>
  <div class="tutorwaiting">
    <div v-for="tutorwaiting in tutorwaitings" :key="tutorwaiting.id">
      <hr />
      <div class="row pointer">
        <div class="col-md-3">
          <nuxt-link :to="'detail/' + tutorwaiting.postId">
            <img class="card-img-left img-fluid" :src="tutorwaiting.announcementpost.imageUrl" alt />
          </nuxt-link>
        </div>

        <div class="col">
          <nuxt-link
            :to="'detail/' + tutorwaiting.postId"
            style="text-decoration: none;
  color: black;"
          >
            <h4 class="title">{{tutorwaiting.announcementpost.name}}</h4>

            <p>{{tutorwaiting.announcementpost.description}}</p>
          </nuxt-link>
        </div>

        <div class="col-2-auto ">
          <nuxt-link
            :to="'detail/' + tutorwaiting.postId"
            style="text-decoration: none;
  color: black;"
          >
            <h4>ประกาศของ</h4>
            <p
              class="card-text"
            >{{ tutorwaiting.announcementpost.tutorName ||'No description provided' }}</p>
          </nuxt-link>
        </div>

        <div class="col-auto ">
          <button class="btn btn-success" @click=" acceptOrder(tutorwaiting.id)">ตอบรับ</button>
          <button class="btn btn-danger" @click=" deleteOrder(tutorwaiting.id)">ยกเลิก</button>
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
  name: "Tutotwaiting",
  props: ["tutorwaitings", "id"],
  data(){
    return{

    }
  },
  methods:{
    async acceptOrder(ids){
      axios.put("http://localhost:1337/orders/"+ids,{
        status:"accept",
        doingstatus:"false"
      })
      this.$router.go(0)
    },
    async deleteOrder(ids) {
      axios
        .delete("http://localhost:1337/orders/" + ids)
        .then(res => {
          console.log("deleteorders success id" + ids);
          console.log(res);
        });
      this.$router.go(0)
    }
  }
};
</script>

