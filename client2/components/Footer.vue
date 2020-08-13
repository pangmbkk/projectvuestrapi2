<template>
  <div>
    <!-- Footer -->
    <footer class="footer text-center">
      <div class="container">
        <ul class="list-inline mb-5">
          <li class="list-inline-item">
            <a class="social-link rounded-circle text-white mr-3" href="https://www.facebook.com/Tutor-Search-244755886571600">
              <font-awesome-icon :icon="['fab', 'facebook-f']" />
            </a>
          </li>
          <li class="list-inline-item">
            <a class="social-link rounded-circle text-white mr-3" href="https://twitter.com/">
              <!-- <i class="icon-social-twitter"></i> -->
              <font-awesome-icon :icon="['fab', 'twitter']" />
            </a>
          </li>
          <li class="list-inline-item">
            <a class="social-link rounded-circle text-white" href="https://github.com/pangmbkk">
              <!-- <i class="icon-social-github"></i> -->
              <font-awesome-icon :icon="['fab','github']" />
            </a>
          </li>
        </ul>
        <p
          class="text-muted small mb-0"
        >Copyright &copy; 5610110734 ERFAN KHARENG DEPARTMENT OF COMPUTER ENGINEERING </p>
        <p class="text-muted small mb-0">PRINCE OF SONGKLA UNIVERSITY HATYAI CAMPUS</p>
      </div>
    </footer>
  </div>
</template>
<style  scoped>
scroll-to-top {
  position: fixed;
  right: 15px;
  bottom: 15px;
  display: none;
  width: 50px;
  height: 50px;
  text-align: center;
  color: white;
  background: rgba(52, 58, 64, 0.5);
  line-height: 45px;
}

.scroll-to-top:focus,
.scroll-to-top:hover {
  color: white;
}

.scroll-to-top:hover {
  background: #343a40;
}

.scroll-to-top i {
  font-weight: 800;
}

footer.footer {
  padding-top: 5rem;
  padding-bottom: 5rem;
}

footer.footer .social-link {
  display: block;
  height: 4rem;
  width: 4rem;
  line-height: 4.3rem;
  font-size: 1.5rem;
  background-color: #1d809f;
  transition: background-color 0.15s ease-in-out;
  box-shadow: 0 3px 3px 0 rgba(0, 0, 0, 0.1);
}

footer.footer .social-link:hover {
  background-color: #155d74;
  text-decoration: none;
}
a {
  color: #1d809f;
}

a:hover,
a:focus,
a:active {
  color: #155d74;
}
</style>
<script>
// import { faChessQueen } from "@fortawesome/free-solid-svg-icons";
// import {fafacebook} from "@fortawesome/free-solid-svg-icons";

export default {
  // computed: {
  //   appIcon() {
  //     return faChessQueen;
  //   },
  //   appIcon2(){
  //     return fafacebook;
  //   }
  // },
};
</script>