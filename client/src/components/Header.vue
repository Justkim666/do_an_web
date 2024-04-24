<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container-fluid">
      <a class="navbar-brand" href="/books">
        <!-- {{ getUser ? (getUser.isAdmin ? 'Thư viện - Admin' : 'Thư viện - User') : 'Thư viện' }} -->
        <ReadFilled/>
      </a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <!-- <li class="nav-item">
            <router-link :to="{ name: 'books' }" class="nav-link active" aria-current="page">Trang chủ</router-link>
  
          </li> -->
          <li class="nav-item">
            <router-link v-if="getUser && getUser.isAdmin" :to="{ name: 'userAdmin' }" class="nav-link active" aria-current="page">Nguời dùng</router-link>
            <!-- <router-link v-else :to="{ name: 'books' }" class="nav-link">Sách</router-link> -->
          </li>
          <li>
            <router-link v-if="getUser && !getUser.isAdmin" :to="{ name: 'profile' }" class="nav-link">Thông tin cá nhân</router-link>
            <router-link v-if="getUser && getUser.isAdmin" :to="{ name: 'bookAdmin' }" class="nav-link">Sách</router-link>
          </li>
          <li class="nav-item">
            <router-link v-if="getUser && !getUser.isAdmin" :to="'/borrowedbooks/' + getUser._id" class="nav-link">Thông tin mượn sách</router-link>
            <router-link v-if="getUser && getUser.isAdmin" :to="{ name: 'publisherAdmin' }" class="nav-link">Nhà xuất bản</router-link>
          </li>
          <li class="nav-item">
            <!-- <router-link v-if="getUser && !getUser.isAdmin" :to="'/borrowedbooks/' + getUser._id" class="nav-link">Theo dõi mượn sách</router-link> -->
            <router-link v-if="getUser && getUser.isAdmin" :to="{ name: 'borrowedBooksAdmin' }" class="nav-link">Theo dõi mượn sách</router-link>
          </li>
        </ul>
        <div class="d-flex">
          <router-link v-if="getUser" :to="{ name: 'books' }" @click="logout" class="btn btn-outline-dark me-2 logout-button">Đăng xuất</router-link>
          <router-link v-if="getUser === null" :to="{ name: 'login' }" class="btn btn-outline-dark me-2">Đăng nhập</router-link>
          <router-link v-if="getUser === null" :to="{ name: 'register' }" class="btn btn-outline-dark">Đăng ký</router-link>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';
import { ReadFilled } from '@ant-design/icons-vue';

export default {
  components: {
    ReadFilled,
    },
  computed: {
    ...mapGetters(['getUser']),
  },
  methods: {
    ...mapActions(['logout']),
    async setUserFromLocalStorage() {
      const userString = localStorage.getItem('user');
      if (userString) {
        const user = JSON.parse(userString);
        await this.$store.commit('SET_USER', user);
      }
    },
  },
  async created() {
    await this.setUserFromLocalStorage();
  },
};
</script>

<style scoped>
.navbar {
  display: flex;
  justify-content: center; /* Căn giữa các phần tử theo chiều ngang */
  align-items: center; /* Căn giữa các phần tử theo chiều dọc */
}

.navbar {
  background: linear-gradient(to right, #ff6f61, #ffca28, #64b5f6); /* Gradient từ cam đến vàng đến xanh dương */
  padding-left: 32px;
  padding-right: 32px;
}


.nav-link {
  margin-right: 15px;
  color: #4a4a4a;
  font-weight: bold;
  border-bottom: 2px solid transparent; /* Thêm border dưới cho liên kết */
  transition: border-color 0.3s ease; /* Thêm hiệu ứng chuyển đổi màu border */
}

.nav-link:hover {
  color: #000;
  text-decoration: none;
  border-color: #fff; /* Thay đổi màu border khi hover vào */
}

.logout-button {
  color: #ffffff; /* Màu chữ trắng */
  font-weight: bold; /* Chữ đậm */
  background-color: #009688; /* Màu xanh lá cây */
  border: 1px solid #009688; /* Viền */
  border-radius: 5px; /* Góc cong */
  padding: 5px 10px; /* Khoảng cách bên trong */
  transition: color 0.3s ease, background-color 0.3s ease; /* Hiệu ứng chuyển đổi màu và nền */
}

.logout-button:hover {
  color: #009688; /* Màu xanh lá cây khi di chuột qua */
  background-color: #ffffff; /* Màu nền trắng */
}

.navbar-brand {
  font-size: 30px; /* Kích thước font */
  font-weight: bold; /* Chữ đậm */
  color: black; /* Màu chữ trắng */
  transition: color 0.3s ease; /* Hiệu ứng chuyển đổi màu chữ */
}

.navbar-brand:hover {
  color: white; /* Màu vàng khi di chuột qua */
}

/* Hiệu ứng cho navbar khi cuộn trang */
.navbar-scrolled {
  background-color: #ff9f51; /* Màu cam nhạt */
}
</style>
