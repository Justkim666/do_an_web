<template>
  <h2 class="center-text">Đăng Nhập</h2>
  <Form @submit="submitLogin" :validation-schema="loginFormSchema">
    <div class="form-group">
      <label for="username">Tên đăng nhập</label>
      <Field name="username" type="text" class="form-control" />
      <ErrorMessage name="username" class="error-feedback" />
    </div>
    <div class="form-group">
      <label for="password">Mật khẩu</label>
      <Field name="password" type="password" class="form-control" />
      <ErrorMessage name="password" class="error-feedback" />
    </div>
    <div class="form-group">
      <button type="submit" class="btn btn-primary">Đăng nhập</button>
    </div>
  </Form>
</template>

<script>
import { Form, Field, ErrorMessage } from "vee-validate";
import * as yup from "yup";
import { loginUser } from "@/services/authService";
import { mapActions, mapGetters } from "vuex";

import VuexStore from "../vuex/store";

export default {
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  store: VuexStore,
  data() {
    return {
      loginFormSchema: yup.object().shape({
        username: yup.string().required("Tên đăng nhập là bắt buộc"),
        password: yup.string().required("Mật khẩu là bắt buộc"),
      }),
    };
  },
  methods: {
    ...mapActions(["setUser"]),
    // ...mapGetters(['getUser']),
    async submitLogin(loginData) {
      try {
        const user = await loginUser(loginData);
        this.setUser(user);
        // console.log('User data:', this.getUser());
        console.log("Đăng nhập thành công!");
        this.$router.push("/books");
      } catch (error) {
        console.error("Đã xảy ra lỗi khi đăng nhập:", error.message);
        // Xử lý lỗi đăng nhập ở đây (hiển thị thông báo lỗi, v.v.)
      }
    },
  },
};
</script>

<style scoped>
  /* Thiết lập font chữ và màu sắc chung */
  body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
  }

  /* Style cho label */
  label {
    font-weight: bold;
    color: #333;
  }

  /* Style cho input */
  .form-control {
    width: 100%;
    padding: 10px;
    margin-top: 5px;
    margin-bottom: 15px;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-sizing: border-box;
    transition: border-color 0.3s ease;
  }

  .form-control:focus {
    border-color: #007bff;
  }

  /* Style cho button */
  .btn-primary {
    padding: 10px 20px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .btn-primary:hover {
    background-color: #0056b3;
    transform: translateY(-2px);
  }

  /* Style cho error message */
  .error-feedback {
    color: red;
    font-size: 14px;
    margin-top: 5px;
    opacity: 0;
    transition: opacity 0.3s ease;
  }

  .form-group:hover .error-feedback {
    opacity: 1;
  }

  /* Style cho form group */
  .form-group {
    margin-bottom: 20px;
  }

  /* Style cho form */
  form {
    max-width: 400px;
    margin: 0 auto;
    background-color: #fff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }

  /* Style cho form title */
  .form-title {
    text-align: center;
    margin-bottom: 20px;
    color: #007bff;
  }

  .center-text {
    text-align: center; /* Căn giữa văn bản theo chiều ngang */
    margin-bottom: 20px; /* Thêm margin bottom cho khoảng cách */
  }
</style>
