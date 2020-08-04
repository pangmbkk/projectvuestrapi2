<template>
  <div>
    <!-- Footer -->
    <footer class="footer text-center">
      <div class="container">
        <ul class="list-inline mb-5">
          <li class="list-inline-item">
            <a class="social-link rounded-circle text-white mr-3" href="#!">
              <i class="icon-social-facebook"></i>
            </a>
          </li>
          <li class="list-inline-item">
            <a class="social-link rounded-circle text-white mr-3" href="#!">
              <i class="icon-social-twitter"></i>
            </a>
          </li>
          <li class="list-inline-item">
            <a class="social-link rounded-circle text-white" href="#!">
              <i class="icon-social-github"></i>
            </a>
          </li>
        </ul>
        <p class="text-muted small mb-0">Copyright &copy; 5610110734 ERFAN KHARENG COMPUTER ENGINEERING PRINCE OF SONGKLA UNIVERSITY HATYAI CAMPUS</p>
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
  color: #1D809F;
}

a:hover, a:focus, a:active {
  color: #155d74;
}
</style>
<script>


export default ({
  
})
</script>