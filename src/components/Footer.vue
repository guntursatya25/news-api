<template>
  <div class="footer-clean">
    <footer>
      <div class="container">
        <div class="row justify-content-flex-start">
          <div class="col-sm-4 col-md-3 item">
            <h3>About</h3>
            <ul>
              <li><a href="#">Company</a></li>
              <li><a href="#">Team</a></li>
              <li><a href="#">Legacy</a></li>
            </ul>
          </div>
          <div class="col-sm-4 col-md-3 item">
            <h3>Careers</h3>
            <ul>
              <li><a href="#">Careers</a></li>
              <li><a href="#">Employee success</a></li>
              <li><a href="#">Benefits</a></li>
            </ul>
          </div>
          <div class="col-lg-6 item social">
            <a href="#"><b-icon-facebook/></a
            ><a href="#"><b-icon-twitter/></a
            ><a href="#"><b-icon-instagram/></a>
            <p class="copyright">News © 2024</p>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: "FooterComponent",
};
</script>

<style>
.footer-clean {
  padding: 50px 0;
  background-color: #fff;
  color: #4b4c4d;
}

.footer-clean h3 {
  margin-top: 0;
  margin-bottom: 12px;
  font-weight: bold;
  font-size: 16px;
}

.footer-clean ul {
  padding: 0;
  list-style: none;
  line-height: 1.6;
  font-size: 14px;
  margin-bottom: 0;
}

.footer-clean ul a {
  color: inherit;
  text-decoration: none;
  opacity: 0.8;
}

.footer-clean ul a:hover {
  opacity: 1;
}

.footer-clean .item.social {
  text-align: right;
}

@media (max-width: 767px) {
  .footer-clean .item {
    text-align: center;
    padding-bottom: 20px;
  }
}

@media (max-width: 768px) {
  .footer-clean .item.social {
    text-align: center;
  }
}

.footer-clean .item.social > a {
  font-size: 24px;
  width: 40px;
  height: 40px;
  line-height: 40px;
  display: inline-block;
  text-align: center;
  border-radius: 50%;
  border: 1px solid #ccc;
  margin-left: 10px;
  margin-top: 22px;
  color: inherit;
  opacity: 0.75;
}

.footer-clean .item.social > a:hover {
  color: #4b4c4d !important;
  opacity: 0.9;
}

@media (max-width: 991px) {
  .footer-clean .item.social > a {
    margin-top: 40px;
  }
}

@media (max-width: 767px) {
  .footer-clean .item.social > a {
    margin-top: 10px;
  }
}

.footer-clean .copyright {
  margin-top: 14px;
  margin-bottom: 0;
  font-size: 13px;
  opacity: 0.6;
}
</style>
