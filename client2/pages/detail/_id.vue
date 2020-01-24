<template>
  <div class="container-fluid">
    <div class="row title align-items-center">
      <div class="col-2"></div>
      <h1 class="text-middle">{{announcementposts.name}}</h1>
    </div>
    <div class="row description">
      <div class="col-2"></div>
      <p>{{announcementposts.description}}</p>
    </div>
    <br />
    <div class="row">
      <!-- <div class="col-1"></div> -->
      <ul class="list-group col-7">
        <li class="list-group-item list-group-item-dark">เนื้อหาและข้อมูลประกอบ</li>
        <li class="list-group-item c1">
          <pre>
            {{detail}}
        </pre>
        </li>
      </ul>
      <ul class="list-group col-5">
        <li class="list-group-item list-group-item-dark">Cras justo odio</li>
        <li class="list-group-item c2">
          <b-media tag="li">
            <template v-slot:aside>
              <b-img blank blank-color="#bac" width="64" alt="placeholder"></b-img>
            </template>

            <h5 class="mt-3 mb-0">List-based media object</h5>
          </b-media>
          <br />
          <form>
            <div class="form-group row">
              <div class="col-1"></div>
              <label for="staticEmail" class="col-sm-2-auto ">วุฒิการศึกษา:</label>
              <div class="col-sm-9">
                <p>ปริญญาตรี คณะวิศกรรมศาสตร์ สงขลานครินทร์ วข.หาดใหญ่</p>
              </div>
            </div>
            <div class="form-group row">
              <div class="col-1"></div>
              <label for="inputPassword" class="col-sm-2-auto ">เบอร์โทรศัพท์:</label>
              <div class="col-sm-9">
                <p>082-4386969</p>
              </div>
            </div>
            <div class="form-group row">
              <div class="col-1"></div>
              <label for="inputPassword" class="col-sm-2-auto ">E-mail:</label>
              <div class="col-sm-9">
                <p>5610110734@psu.ac.th</p>
              </div>
            </div>
            <div class="form-group row">
              <div class="col-1"></div>
              <label for="inputPassword" class="col-sm-2-auto ">ประสบการณ์:</label>
              <div class="col-sm-9">
                <p>5 ปี</p>
              </div>
            </div>
            <div class="form-group row">
              <div class="col-1"></div>
              <label for="inputPassword" class="col-sm-2-auto ">จังหวัด:</label>
              <div class="col-sm-9">
                <p>สงขลา</p>
              </div>
            </div>
             
             <div class="form-group row">
              <div class="col-1"></div>
              <label for="inputPassword" class="col-sm-2-auto ">เขต/อำเภอ:</label>
              <div class="col-sm-9">
                <p>หาดใหญ่</p>
              </div>
            </div>
          </form>
          
        </li>
      </ul>
      <!-- <div class="col-1"></div> -->
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data(){
    return{
      announcementposts:[],
      detail:null,
    }
  },
  async created(){
    axios.get("http://localhost:1337/announcementposts/"+this.$route.params.id).then(res => {
      this.announcementposts = res.data;
      this.detail = res.data.detail;
      console.log("get announcementposts success");
    });
  }
};

</script>

<style scoped>
.title {
  background-color: #29303B;
  color: aliceblue;
  height: 5rem;
}
.description{
  background-color: #29303B;
  color: aliceblue;
  height: 3rem;
}
.col-7 {
  padding-left: 2rem;
  padding-right: 1rem;
  padding-bottom: 2rem;
}
.col-5 {
  padding-left: 1rem;
  padding-right: 2rem;
  padding-bottom: 2rem;
}
.c1 {
  height: 100%;
}
.c2 {
  height: 90%;
}

</style>
