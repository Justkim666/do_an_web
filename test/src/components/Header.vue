

<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container">
      <router-link to="/" class="navbar-brand">Thư Viện</router-link>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link to="/" class="nav-link" aria-current="page">Trang chủ</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/books" class="nav-link">Sách</router-link>
          </li>
        </ul>
        <!-- Thay đổi nút Search thành Đăng nhập và Đăng ký -->
        <div class="d-flex">
          <!-- <router-link to="/login" class="btn btn-outline-dark me-2">Đăng nhập</router-link> -->
          <router-link :to="{ name: 'register' }" class="btn btn-outline-dark">Đăng ký</router-link>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import { RouterLink } from 'vue-router'
export default {
  name: 'Header'
}
</script>

<style scoped>
/* Thêm CSS tùy chỉnh cho header */
</style>
