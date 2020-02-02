<template>
  <div class="container">
    <br />
    <h3 class="text-center">ลงทะเบียนติวเตอร์</h3>

    <div class="row">
      <div class="col-2"></div>
      <form class="col form1">
        <br />

        <div class="f์orm-group row">
          <label for="staticEmail" class="col-sm-2 col-form-label">ชื่อหัวข้อ</label>
          <div class="col-sm-10">
             <b-form-input size="sm" placeholder="กรอกชื่อหัวข้อ" v-model="name"></b-form-input>
          </div>
        </div>
        <br />
        <div class="f์orm-group row">
          <label for="staticEmail" class="col-sm-2 col-form-label">รายละเอียด</label>
          <div class="col-sm-10">
            <b-form-input  size="sm" placeholder="กรอกรายละเอียดสั้นๆ" v-model="description"></b-form-input>
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
            <b-form-select v-model="subjectname" size="sm">
              <option :value="null">--เลือกวิชา--</option>
              <option
                v-for="subjectname in subjectnames"
                :key="subjectname.id"
                :value="subjectname.name"
              >{{subjectname.name}}</option>
            </b-form-select>
          </div>
        </div>
        <div class="form-group row">
          <label for="inputPassword" class="col-sm-2 col-form-label">ระดับชั้น</label>
          <div class="col-sm-10">
            <b-form-select v-model="educationlevel" size="sm">
              <option :value="null">--เลือกระดับชั้น--</option>
              <option
                v-for="educationlevel in educationlevels"
                :key="educationlevel.id"
                :value="educationlevel.name"
              >{{educationlevel.name}}</option>
            </b-form-select>
          </div>
        </div>
        <div class="form-group row">
          <label for="inputPassword" class="col-sm-2 col-form-label">ประสบการณ์ผู้สอน</label>
          <div class="col-sm-10">
            <b-form-select v-model="experience" size="sm">
              <option :value="null">--เลือกประสบการณ์ผู้สอน--</option>
              <option
                v-for="experience in experiences"
                :key="experience.id"
                :value="experience.name"
              >{{experience.name}}</option>
            </b-form-select>
          </div>
        </div>
        <div class="f์orm-group row">
          <label for="staticEmail" class="col-sm-2 col-form-label">เนื้อหา</label>
          <div class="col-sm-10">
            <b-form-textarea id="textarea-small" size="sm" placeholder="กรอกข้อมูลรายละเอียดและเนื้อหา" v-model="detail"></b-form-textarea>
          </div>
        </div>
        <br />
        <div class="f์orm-group row">
          <label for="staticEmail" class="col-sm-2 col-form-label">รูปภาพประกรอบ</label>
          <div class="col-sm-10">
            <b-form-file id="file-small" size="sm"  v-model="image" @change="onFileSelected"></b-form-file>
          </div>
        </div>
        <br />
        <div class="form-group row">
          <label for="inputPassword" class="col-sm-2 col-form-label">จังหวัด</label>
          <div class="col-sm-10">
            <b-form-select v-model="province" size="sm">
              <option :value="null">--เลือกจังหวัดที่ต้องการ--</option>
              <option
                v-for="province in provinces"
                :key="province.id"
                :value="province.name"
              >{{province.name}}</option>
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
      selectedFile:null,
      name: "",
      description: "",
      detail: "",
      image: "",
      educationlevels: "",
      educationlevel: null,
      subjectnames: "",
      subjectname: null,
      experiences: "",
      experience: null,
      provinces:"",
      province:null,
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
  async created() {
    axios.get("http://localhost:1337/educationlevels").then(response => {
      this.educationlevels = response.data;
      console.log(this.educationlevels);
      console.log("get educationlevels");
    });
    axios.get("http://localhost:1337/subjectnames").then(response => {
      this.subjectnames = response.data;
      console.log(this.subjectnames);
      console.log("get subjectnames");
    });
    axios.get("http://localhost:1337/experiences").then(response => {
      this.experiences = response.data;
      console.log(this.experiences);
      console.log("get experiences");
    });
    axios.get("http://localhost:1337/provinces").then(response => {
      this.provinces = response.data
      console.log("get province")
    })
  },
  methods: {
    onFileSelected(event){
      console.log(event)
      this.selectedFile = event.target.files[0]
    },
    onSubmit() {
      axios
        .post("http://localhost:1337/tests", {
          name: this.name,
          num: this.num
        })
        .then(response => {
          console.log(response);
        });
    }
  },
  computed: {}
};
</script>

