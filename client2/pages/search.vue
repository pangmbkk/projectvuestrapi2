<template>
  <div class="bodynon">
    <div class="container-fluid row">
      <div class="container">
        <br />
        <form @submit.prevent="onSearch()">
          <div class="form-group row">
            <!-- ฟอรม เลือก จังหวัด-->
            <div class="col-1"></div>

            <div class="col-4">
              <b-form-select v-model="province" size="sm">
                <option :value="null">--เลือกจังหวัดของคุณ--</option>
                <option
                  v-for="province in provinces"
                  :key="province.id"
                  :value="province.name"
                >{{province.name}}</option>
              </b-form-select>
            </div>
            <div class="col-4">
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
          <!-- จบform -->
          <div class="form-group row">
            <div class="col-1"></div>

            <div class="col-4">
              <b-form-select v-model="educationlevel" size="sm">
                <option :value="null">--ระดับชั้น--</option>
                <option
                  v-for="educationlevel in educationlevels"
                  :key="educationlevel.id"
                  :value="educationlevel.name"
                >{{educationlevel.name}}</option>
              </b-form-select>
            </div>
            <div class="col-4">
              <b-form-select v-model="experience" size="sm">
                <option :value="null">--เลือกประสบการณ์ผู้สอน--</option>
                <option
                  v-for="experience in experiences"
                  :key="experience.id"
                  :value="experience.name"
                >{{experience.name}}</option>
              </b-form-select>
            </div>

            <button
              class="btn btn-primary btn-sm col"
              v-on:click.stop.prevent="onSearch(province,subjectname,educationlevel,experience)"
            >ค้นหา</button>
          </div>
        </form>
      </div>
      <!--จบcontainer -->
    </div>
    <!--จบcontainer-fluid -->

    <div class="container-fluid body">
      <div class="container">
        <br />
        <div class="row">
          <div class="col-md-9">
            <div>
              <Listsearch
                class="router"
                v-for="listsearch in listsearchs"
                :key="listsearch.id"
                :id="listsearch.id"
                :listsearch="listsearch"
              />
            </div>
          </div>

          <div class="col-md-3">
            <hr />
            <ul class="list-group">
              <li class="list-group-item texbox">
                <h5>วิธีการใช้งานเว็บไซต์</h5>
                <p>-------------------------------------------</p>
              </li>
            </ul>
            <br />
            <ul class="list-group">
              <li class="list-group-item texbox">
                <h5>วิธีการใช้งานเว็บไซต์</h5>
                <p>-------------------------------------------</p>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.router {
  text-decoration: none;
  color: black;
}

.bodynon {
  background-color: #2c3e50 !important;
}
.texbox {
  background-color: none;
}
.body {
  background-color: white;
}
img {
  margin-bottom: 5px;
  margin-top: 5px;
  border: 0;
  width: 50;
  max-width: 100%;
  height: auto;
}
.pointer {
  cursor: pointer;
}
</style>

<script>
// @ is an alias to /src
import Strapi from "strapi-sdk-javascript/build/main";
import axios from "axios";
const apiUrl = process.env.API_URL || "http://localhost:1337";
const strapi = new Strapi(apiUrl);
import Listsearch from "../components/Listsearch";

export default {
  components: {
    Listsearch
  },

  data() {
    return {
      listsearchs: [],
      infos: [],
      info: {
        id: "0",
        name: "",
        description: ""
      },
      provinces: [],
      province: null,
      subjectnames: [],
      subjectname: null,
      educationlevels: [],
      educationlevel: null,
      experiences:[],
      experience:null,

    };
  },
  async created() {
    axios.get("http://localhost:1337/announcementposts").then(response => {
      this.listsearchs = response.data;
      console.log("get Announcementposts success");
      
    });
    axios.get("http://localhost:1337/provinces").then(res => {
      this.provinces = res.data;
      console.log("get provinces success");
    });
    axios.get("http://localhost:1337/subjectnames").then(res => {
      this.subjectnames = res.data;
      console.log("get subjectnames success");
    });
    axios.get("http://localhost:1337/educationlevels ").then(res => {
      this.educationlevels = res.data;
      console.log("get educationlevels success");
    }); 
     axios.get("http://localhost:1337/experiences ").then(res => {
      this.experiences = res.data;
      console.log("get experiences success");
    });
  },
  methods: {
    
    async onSearch(searchedprovicetype, searchedsubjecttype,searchededucationleveltype,searchedexperiencetype) {
      if(searchedprovicetype==null && searchedsubjecttype==null && searchededucationleveltype == null && searchedexperiencetype==null){
         axios.get("http://localhost:1337/announcementposts").then(response => {
          this.listsearchs = response.data;
         
          console.log("get onS.allapiAnnouncementposts success");
        });
       
      }
      else if (searchedprovicetype != null && searchedsubjecttype==null && searchededucationleveltype == null && searchedexperiencetype==null) {
        axios
          .get("http://localhost:1337/announcementposts?provinceName="+ this.province).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch province success");
          });
          return;
      }
      else if(searchedprovicetype == null && searchedsubjecttype!=null  && searchededucationleveltype == null && searchedexperiencetype==null) {
         axios
          .get("http://localhost:1337/announcementposts?subjectName="+ this.subjectname).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch subjectname success");
          });
          return;
      }
      else if(searchedprovicetype == null && searchedsubjecttype==null  && searchededucationleveltype != null && searchedexperiencetype==null) {
         axios
          .get("http://localhost:1337/announcementposts?educationName="+ this.educationlevel).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch educationlevel success");
          });
          return;
      } else if(searchedprovicetype == null && searchedsubjecttype==null  && searchededucationleveltype == null && searchedexperiencetype!=null) {
         axios
          .get("http://localhost:1337/announcementposts?experienceName="+ this.experience).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch experience success");
          });
          return;
      }
      else if(searchedprovicetype != null && searchedsubjecttype!=null && searchededucationleveltype == null && searchedexperiencetype == null ){
         axios
          .get("http://localhost:1337/announcementposts?subjectName_in="+ this.subjectname + "&provinceName_in="+this.province ).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch province subjectname success both");
          });
          return;
      }else if(searchedprovicetype != null && searchedsubjecttype==null && searchededucationleveltype != null && searchedexperiencetype == null ){
         axios
          .get("http://localhost:1337/announcementposts?educationName_in="+ this.educationlevel + "&provinceName_in="+this.province ).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch province educationlevel success both");
          });
          return;
      }
      else if(searchedprovicetype != null && searchedsubjecttype==null && searchededucationleveltype == null && searchedexperiencetype != null ){
         axios
          .get("http://localhost:1337/announcementposts?educationName_in="+ this.experience + "&provinceName_in="+this.province ).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch province experience success both");
          });
          return;
      }
      else if(searchedprovicetype == null && searchedsubjecttype!=null && searchededucationleveltype != null && searchedexperiencetype == null ){
         axios
          .get("http://localhost:1337/announcementposts?educationName_in="+ this.educationlevel + "&subjectName_in="+this.subjectname ).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch subjectname educationlevel success both");
          });
          return;
      }
      else if(searchedprovicetype == null && searchedsubjecttype!=null && searchededucationleveltype == null && searchedexperiencetype != null ){
         axios
          .get("http://localhost:1337/announcementposts?educationName_in="+ this.experience + "&subjectName_in="+this.subjectname ).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch subjectname experience success both");
          });
          return;
      }
      else if(searchedprovicetype == null && searchedsubjecttype==null && searchededucationleveltype != null && searchedexperiencetype != null ){
         axios
          .get("http://localhost:1337/announcementposts?experienceName_in="+ this.experience + "&educationName_in="+this.educationlevel ).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch educationlevel experience success both");
          });
          return;
      }
      else if(searchedprovicetype != null && searchedsubjecttype!=null && searchededucationleveltype != null && searchedexperiencetype == null ){
         axios
          .get("http://localhost:1337/announcementposts?provinceName_in="+ this.province + "&subjectName_in="+this.subjectname + "&educationName_in="+this.educationlevel ).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch province subjectname educationlevel success 3api");
          });
          return;
      }
      else if(searchedprovicetype != null && searchedsubjecttype!=null && searchededucationleveltype == null && searchedexperiencetype != null ){
         axios
          .get("http://localhost:1337/announcementposts?provinceName_in="+ this.province + "&subjectName_in="+this.subjectname + "&experienceName_in="+this.experience ).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch province subjectname experience success 3api");
          });
          return;
      }
      else if(searchedprovicetype != null && searchedsubjecttype==null && searchededucationleveltype != null && searchedexperiencetype != null ){
         axios
          .get("http://localhost:1337/announcementposts?provinceName_in="+ this.province + "&educationName_in="+this.educationlevel + "&experienceName_in="+this.experience ).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch province educationlevel experience success 3api");
          });
          return;
      }
      else if(searchedprovicetype == null && searchedsubjecttype!=null && searchededucationleveltype != null && searchedexperiencetype != null ){
         axios
          .get("http://localhost:1337/announcementposts?subjectName_in="+ this.subjectname + "&educationName_in="+this.educationlevel + "&experienceName_in="+this.experience ).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch subjectname educationlevel experience success 3api");
          });
          return;
      }
      else if(searchedprovicetype != null && searchedsubjecttype!=null && searchededucationleveltype != null && searchedexperiencetype != null ){
         axios
          .get("http://localhost:1337/announcementposts?provinceName_in="+ this.province + "&subjectName_in="+this.subjectname + "&educationName_in="+this.educationlevel + "&experienceName_in="+this.experience ).then(response => {
            this.listsearchs = response.data;
            console.log("get onsearch province subjectname educationlevel experience success 4api");
          });
          return;
      }
      

    }
  }
};
</script>
