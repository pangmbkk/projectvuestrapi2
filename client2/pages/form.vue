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
            <b-form-input size="sm" placeholder="กรอกรายละเอียดสั้นๆ" v-model="description"></b-form-input>
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
            <b-form-textarea
              id="textarea-small"
              size="sm"
              placeholder="กรอกข้อมูลรายละเอียดและเนื้อหา"
              v-model="detail"
            ></b-form-textarea>
          </div>
        </div>
        <br />
        <div class="f์orm-group row">
          <label for="staticEmail" class="col-sm-2 col-form-label">รูปภาพประกรอบ</label>
          <div class="col-sm-10">
            <b-form-file id="file-small" size="sm" @change="onFileSelected"></b-form-file>
          </div>
        </div>
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
        <div class="f์orm-group row">
          <label for="staticEmail" class="col-sm-2 col-form-label">ชื่อ-สกุล</label>
          <div class="col-sm-10">
            <b-form-input size="sm" placeholder="กรอกชื่อและนามสกุล" v-model="tutorname"></b-form-input>
          </div>
        </div>
        <br />
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
import { mapMutations } from "vuex";
export default {
  computed: {
    username() {
      return this.$store.getters["auth/username"];
    },
    tutoruser(){
      return this.$store.getters["auth/tutoruser"];
    }
  },
  data() {
    return {
      selectedImage: null,
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
      provinces: "",
      province: null,
      tutorname:null,
      userNname:null,
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
      this.provinces = response.data;
      console.log("get province");
    });
  },
  methods: {
    onFileSelected(event) {
      console.log(event);
      this.selectedImage = event.target.files[0];
    },
    onUpload() {
      // const formData = new FormData();
      // formData.append("files", this.selectedImage, this.selectedImage.name);
      // const file = strapi.upload(formData).then(res => {
      //   console.log(res[0].url);
      //   this.image = `http://localhost:1337${res[0].url}`;
      //   console.log(this.image);
      // });
    },
    // `File name: ${file}`
    onSubmit() {
      const formData = new FormData();
      formData.append("files", this.selectedImage, this.selectedImage.name);
      const file = strapi.upload(formData).then(res => {
        console.log(res[0])
        console.log(res[0].url);
        this.image = `http://localhost:1337${res[0].url}`;
        console.log(this.image);
        axios
        .post("http://localhost:1337/announcementposts", {
          name: this.name,
          description: this.description,
          provinceName: this.province,
          subjectName: this.subjectname,
          educationName: this.educationlevel,
          experienceName: this.experience,
          detail: this.detail,
          tutorName:this.tutorname,
          username:this.username,
          imageUrl: this.image,
          email:this.tutoruser.email, 
        })
        .then(response => {
          console.log(response);
          // location.replace("http://localhost:3000/listPostmanage")
          this.$router.back()
        });
      });
      
      
    }
  }
};
</script>

