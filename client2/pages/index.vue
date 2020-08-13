<template>
  <div class="home">
    <header class="masthead d-flex">
      <div class="container text-center my-auto">
        <h1 class="mb-1">ค้นหาติวเตอร์</h1>
        <h3 class="mb-5">
          <em>A Free Bootstrap Theme by Start Bootstrap</em>
        </h3>
        <a class="btn btn-primary btn-xl js-scroll-trigger" href="#about">ลงทะเบียน</a>
      </div>
      <div class="overlay"></div>
    </header>
    <!-- About -->
    <section class="content-section bg-light" id="about">
      <div class="container text-center">
        <div class="row">
          <div class="col-lg-6 mx-auto">
            
            <h2>ผู้เรียน</h2>

            <p class="lead mb-5">
              This theme features a flexible, UX friendly sidebar menu and stock photos from our friends at
              <a
                href="https://unsplash.com/"
              >Unsplash</a>!
            </p>
          </div>
          <div class="col-lg-6 mx-auto">
            
            <h2>ติวเตอร์</h2>

            <p class="lead mb-5">
              This theme features a flexible, UX friendly sidebar menu and stock photos from our friends at
              <a
                href="https://unsplash.com/"
              >Unsplash</a>!
            </p>
          </div>
        </div>
            <a class="btn btn-dark btn-xl js-scroll-trigger" href="#services">What We Offer</a>

      </div>
    </section>

    <!-- Services -->
    <section class="content-section bg-primary text-white text-center" id="services">
      <div class="container">
        <div class="content-section-heading">
          <!-- <h3 class="text-secondary mb-0">Services</h3>   -->
          <h2 class="mb-5">วิธีการใช้งานเว็บไซต์</h2>
        </div>
        <div class="row">
          <div class="col-lg-3 col-md-6 mb-5 mb-lg-0">
            <span class="service-icon rounded-circle mx-auto mb-3">
              <i class="icon-screen-smartphone"></i>
            </span>
            <h4>
              <strong>Responsive</strong>
            </h4>
            <p class="text-faded mb-0">Looks great on any screen size!</p>
          </div>
          <div class="col-lg-3 col-md-6 mb-5 mb-lg-0">
            <span class="service-icon rounded-circle mx-auto mb-3">
              <i class="icon-pencil"></i>
            </span>
            <h4>
              <strong>Redesigned</strong>
            </h4>
            <p class="text-faded mb-0">Freshly redesigned for Bootstrap 4.</p>
          </div>
          <div class="col-lg-3 col-md-6 mb-5 mb-md-0">
            <span class="service-icon rounded-circle mx-auto mb-3">
              <i class="icon-like"></i>
            </span>
            <h4>
              <strong>Favorited</strong>
            </h4>
            <p class="text-faded mb-0">
              Millions of users
              <i class="fas fa-heart"></i>
              Start Bootstrap!
            </p>
          </div>
          <div class="col-lg-3 col-md-6">
            <span class="service-icon rounded-circle mx-auto mb-3">
              <i class="icon-mustache"></i>
             
                <font-awesome-icon far icon="spinner" />
            </span>
            <h4>
              <strong>Question</strong>
            </h4>
            <p class="text-faded mb-0">I mustache you a question...</p>
          </div>
        </div>
      </div>
    </section>


  </div>
</template>
<script>
import Strapi from "strapi-sdk-javascript/build/main";
import axios from "axios";
const apiUrl = process.env.API_URL || "http://localhost:1337";
const strapi = new Strapi(apiUrl);

export default {
  data() {
    return {
      query: "",
      provinces: [],
      province: null,
      subjectnames: [],
      subjectname: null,
      educationlevels: [],
      educationlevel: null,
      subjurls: [
        {
          id: "1",
          url:
            "https://www.google.com/url?sa=i&source=images&cd=&cad=rja&uact=8&ved=2ahUKEwizk-uhvYPnAhUl6nMBHVQ4BL8QjRx6BAgBEAQ&url=https%3A%2F%2Fsites.google.com%2Fa%2Fsamakkhi.ac.th%2Fkeiyw-kab-phasa-thiy&psig=AOvVaw1Nf7g3_4mKI1DkisQ1JQm6&ust=1579104492976330",
        },
      ],
    };
  },
  async created() {
    axios.get("http://localhost:1337/provinces").then((res) => {
      this.provinces = res.data;
      console.log("get provinces success");
    });
    axios.get("http://localhost:1337/subjectnames").then((res) => {
      this.subjectnames = res.data;
      console.log("get subjectnames success");
    });
    axios.get("http://localhost:1337/educationlevels ").then((res) => {
      this.educationlevels = res.data;
      console.log("get educationlevels success");
    });
  },
  computed: {
    filteredList() {
      return this.restaurants.filter((restaurant) => {
        return restaurant.name.toLowerCase().includes(this.query.toLowerCase());
      });
    },
    restaurants() {
      return this.$store.getters["restaurants/list"];
    },
  },
};
</script>

<style scoped>
.home {
  width: 100%;
  height: 100%;
}
.btn-xl {
  padding: 1.25rem 2.5rem;
}

.content-section {
  padding-top: 7.5rem;
  padding-bottom: 7.5rem;
}

.content-section-heading h2 {
  font-size: 3rem;
}

.content-section-heading h3 {
  font-size: 1rem;
  text-transform: uppercase;
}
h1,
h2,
h3,
h4,
h5,
h6 {
  font-weight: 700;
}

.text-faded {
  color: rgba(255, 255, 255, 0.7);
}

/* ยังไม่เพิ่ม */


.masthead {
  min-height: 30rem;
  position: relative;
  display: table;
  width: 100%;
  height: auto;
  padding-top: 8rem;
  padding-bottom: 8rem;
  background: linear-gradient(
      90deg,
      rgba(255, 255, 255, 0.1) 0%,
      rgba(255, 255, 255, 0.1) 100%
    ),
    url("../assets/img/bg-masthead.jpg");
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
}

.masthead h1 {
  font-size: 4rem;
  margin: 0;
  padding: 0;
}
@media (min-width: 992px) {
  .masthead {
    height: 100vh;
  }
  .masthead h1 {
    font-size: 5.5rem;
  }
}

.service-icon {
  background-color: #fff;
  color: #1D809F;
  height: 7rem;
  width: 7rem;
  display: block;
  line-height: 7.5rem;
  font-size: 2.25rem;
  box-shadow: 0 3px 3px 0 rgba(0, 0, 0, 0.1);
}
a {
  color: #1D809F;
}

a:hover, a:focus, a:active {
  color: #155d74;
}

.btn-primary {
  background-color: #1D809F !important;
  border-color: #1D809F !important;
  color: #fff !important;
}

.btn-primary:hover, .btn-primary:focus, .btn-primary:active {
  background-color: #155d74 !important;
  border-color: #155d74 !important;
}

.btn-secondary {
  background-color: #ecb807 !important;
  border-color: #ecb807 !important;
  color: #fff !important;
}

.btn-secondary:hover, .btn-secondary:focus, .btn-secondary:active {
  background-color: #ba9106 !important;
  border-color: #ba9106 !important;
}

.btn-dark {
  color: #fff !important;
}

.btn {
  box-shadow: 0px 3px 3px 0px rgba(0, 0, 0, 0.1);
  font-weight: 700;
}

.bg-primary {
  background-color: #1D809F !important;
}

.text-primary {
  color: #1D809F !important;
}

.text-secondary {
  color: #ecb807 !important;
}


/* .card {
  margin: 10px;
}
.slide2 {
  background-color: #2c3e50;
}
.form-control {
  margin-right: 30px;
} */
/* .dropdownleft {
  margin-left: 15px;
  แท็บดรอปดาวไปขวามานิดนึง
} */
/* .btn {
  margin-left: 8px;
  margin-right: 15px;
}

.body {
  background-color: white;
} */
</style>

