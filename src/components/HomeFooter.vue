<template>
  <div>
    <footer class="footer py-3 mt-5">
      <div class="container">
        <ul class="list-inline text-center contact-info mb-1">
          <li class="list-inline-item">
            <a href="#" class="text-primary"><i class="fab fa-github text-secondary text-muted"></i></a>
          </li>
          <li class="list-inline-item">
            <a href="#" class="text-primary"
              ><i class="fab fa-instagram text-secondary text-muted"></i
            ></a>
          </li>
          <li class="list-inline-item">
            <a href="#" class="text-primary"
              ><i class="fab fa-facebook-f text-secondary text-muted"></i
            ></a>
          </li>
          <li class="list-inline-item">
            <a
              href="mailto:a68b58@gmail.com"
              type="mail"
              class="text-primary"
              ><i class="fas fa-envelope text-secondary text-muted"></i
            ></a>
          </li>
        </ul>
        <p class="text-center copyright">
          ©Copright 2020 Produeced by
          <a href="mailto:a68b58@gmail.com" type="mail">Sandy Zheng</a>
        </p>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'HomeFooter',
}
</script>

<style lang="scss" scoped>
.footer {
    border-top: 1px solid gray;
}
.contact-info {
    margin-bottom: 5px;
    margin-top: 15px;
    li {
      font-size: 1.7rem;
      height: 50px;
      width: 50px;
    }
}
.copyright {
  color: gray;
  font-size: 0.8rem;
  a {
    color: gray;
  }
}
</style>