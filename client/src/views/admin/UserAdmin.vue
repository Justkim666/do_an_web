<template>
  <div>
    <h4 class="center-text">QUẢN LÝ NGƯỜI DÙNG</h4>
    <div class="action-button">
      <router-link :to="{ name: 'addUser' }" class="btn btn-add">Thêm người dùng mới</router-link>
    </div>
    
    <table class="table">
      <thead>
        <tr>
          <th>ID</th>
          <th>Tên đăng nhập</th>
          <th>Tên</th>
          <th>Số điện thoại</th>
          <th>Địa chỉ</th>
          <th>Chức vụ</th>
          <th></th>
          <!-- Add more columns as needed -->
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <td>{{ user._id }}</td>
          <td>{{ user.username }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.phone }}</td>
          <td>{{ user.address }}</td>
          <td>{{ user.isAdmin ? 'Admin' : 'User' }}</td>
          <td>
              <router-link :to="'/admin/edituser/' + user._id" class="btn btn-edit">Sửa</router-link>
              <button class="btn btn-delete" @click="deleteUser(user)">Xóa</button>
          </td>
          <!-- Add more cells as needed -->
        </tr>
      </tbody>
    </table>
  </div>
</template>
  
<script>
import { getAllUsers, deleteUser as apiDeleteUser } from '@/services/userService';

export default {
  data() {
    return {
      users: [],
    };
  },
  methods: {
    editUser(user) {
      // Handle the edit user action here
    },
    async deleteUser(user) {
      if (window.confirm('Bạn có chắc chắn muốn xóa người dùng này không?')) {
        try {
          const token = localStorage.getItem('token'); // Replace with your token
          await apiDeleteUser(user._id, token);
          this.users = this.users.filter(u => u._id !== user._id);
        } catch (error) {
          console.error(error);
        }
      }
    },
  },
  async created() {
    try {
      const token = localStorage.getItem('token'); // Replace with your token
      this.users = await getAllUsers(token);
    } catch (error) {
      console.error(error);
    }
  },
};
</script>

  
  <style scoped>

  .action-button {
    text-align: right; /* Đặt nút ở bên phải */
    margin-bottom: 1em; /* Thêm margin bottom */
  }

  .table {
    width: 100%;
    margin-top: 1em;
    border-collapse: collapse;
  }
  
  .table th, .table td {
    border: 1px solid #ddd;
    padding: 8px;
  }
  
  .table th {
    padding-top: 12px;
    padding-bottom: 12px;
    text-align: left;
    background-color: #F8F9FA;
    color: black;
  }
  .btn {
    padding: 5px 10px;
    margin: 5px;  
    border: none;
    cursor: pointer;
    border-radius: 5px;
    font-size: 14px;
  }

  .btn-add {
    background-color: #0082CC;  
    color: white;
    margin-bottom: 1em;
    font-size: 15px;  
    padding: 10px 20px;  
    box-shadow: 0 5px 15px rgba(0,0,0,0.2);  
    transition: all 0.3s ease;  
    text-align: right;
  }

  .btn-add:hover {
    background-color: #005999;  
    box-shadow: 0 5px 15px rgba(0,0,0,0.3); 
  }
  .btn-edit {
    background-color: #4CAF50;
    color: white;
  }

  .btn-delete {
    background-color: #f44336;
    color: white;
  }

  .center-text {
    text-align: center; /* Căn giữa văn bản theo chiều ngang */
    margin-bottom: 20px; /* Thêm margin bottom cho khoảng cách */
  }
  </style>