<template>
  <div class="container">
    <br />
    <h3 class="text-center">สร้างฟอร์ม</h3>

    <div class="row">
      <div class="col-2"></div>
      <form class="col form1">
        <br />

        <div class="f์orm-group row">
          <label for="staticEmail" class="col-sm-2 col-form-label">ชื่อประกาศ</label>
          <div class="col-sm-10">
            <input type="text" class="form-control" placeholder="กรอกชื่อประกาศ" v-model="name" />
          </div>
        </div>
        <br />

        <!-- <div class="form-group row">
                <label for="inputPassword" class="col-sm-2 col-form-label">รายละเอียด</label>
                <div class="col-sm-10">
                <input type="text" class="form-control"  placeholder="กรอกรายละเอียด" v-model="description" >
                </div>
        </div>-->
        <div class="form-group row">
          <label for="inputPassword" class="col-sm-2 col-form-label">วิชา</label>
          <div class="col-sm-10">
            <b-form-select v-model="num" size="sm">
              <option :value="null">--ระดับชั้น--</option>
              <option v-for="num in nums" :key="num.id" :value="num.num">{{num.num}}</option>
            </b-form-select>
          </div>
        </div>
        <!-- <div class="form-group row">
                <label for="inputPassword" class="col-sm-2 col-form-label">ระดับชั้น</label>
                <div class="col-sm-10">
                <select class="form-control" id="exampleFormControlSelect1">
                    <option>1</option>
                    <option>2</option>
                    <option>3</option>
                    <option>4</option>
                    <option>5</option>
                </select>
                </div>
        </div>-->
        <!-- <div class="form-group row">
                <label for="inputPassword" class="col-sm-2 col-form-label">เนื้อหา</label>
                <div class="col-sm-10">
                <textarea class="form-control" id="exampleFormControlTextarea1" rows="3"></textarea>
                </div>
        </div>-->
        <div class="form-group row">
          <button
            class="btn btn-primary btn-block"
            v-on:click.stop.prevent="onSubmit()"
            type="submit"
          >ยืนยัน</button>
        </div>
      </form>
      <div class="col-3"></div>
    </div>
  </div>
</template>
<style scoped>
</style>
<script>
import Strapi from "strapi-sdk-javascript/build/main";
const apiUrl = process.env.API_URL || "http://localhost:1337";
const strapi = new Strapi(apiUrl);
import axios from "axios";
export default {
  data() {
    return {
      name: "555",
      description: "555",
      num: null,
      nums: [
        {
          id: 1,
          num: 2
        },
        {
          id: 2,
          num: 3
        }
      ]
    };
  },
  methods: {
    onSubmit() {
      axios.post("http://localhost:1337/tests",{
          name:this.name,
          num:this.num

      }).then(response => {
        console.log(response);
      });
     
    }
  },
  computed: {}
};
</script>

