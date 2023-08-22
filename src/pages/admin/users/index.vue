<template>
    <div>
      <a-card title="Tài khoản" style="width: 100%">
        <div class="row mb-3">
          <div class="col-12 d-flex justify-content-end">
            <a-button type="primary">
              <router-link :to="{ name: 'admin-users-create' }">
              <font-awesome-icon :icon="['fas', 'plus']" />
              </router-link>            
            </a-button>
          </div>
        </div>

        <div class="row">
          <div class="col-12">
            <a-table :dataSource="users" :columns="columns" :scroll="{ x: 576 }">
              <template #bodyCell="{ column, index, record }">
                <template v-if="column.key === 'index'">
                  <span>{{ index + 1 }}</span>
                </template>
                <template v-if="column.key === 'status'">
                  <span v-if="record.status_id == 1" class="text-primary">{{ record.status }}</span>
                  <span v-else-if="record.status_id == 2" class="text-danger">{{ record.status }}</span>
                </template>
              </template>
            </a-table>
          </div>
        </div>
      </a-card>
    </div>
  </template>
  
  <script>
  import { defineComponent, ref } from 'vue';  
  import { useMenu } from '../../../stores/use-menu';
  
  export default defineComponent ({
    setup() {
      useMenu().onSelectedKeys(['admin-users']);
      
      const users = ref([]);
      const columns = [
        {
          title: '#',
          key: 'index',
        },
        {
          title: 'Avatar',
          dataIndex: 'avatar',
          key: 'avatar',
        },
        {
          title: 'Tài khoản',
          dataIndex: 'username',
          key: 'username',
        },
        {
          title: 'Họ Tên',
          dataIndex: 'name',
          key: 'name',
        },
        {
          title: 'Tài khoản',
          dataIndex: 'username',
          key: 'username',
        },
        {
          title: 'Phòng Ban',
          dataIndex: 'departments',
          key: 'departments',
          response: ['sm'],
        },
        {
          title: 'Vai trò',
          key: 'roles',
        },
        {
          title: 'Tình trạng',
          dataIndex: 'status',
          key: 'status',
        },
        {
          title: 'Công cụ',
          key: 'action',
          fixed: 'right'
        },
      ]

      const getUsers = () => {
        axios.get('http://127.0.0.1:8000/api/users')
          .then((response) => {
            users.value = response.data;
          })
          .catch((error) => {
            console.log(error);
          });
      };
      
      getUsers();

      return {
        users,
        columns
      }
    },
  });
  </script>
  