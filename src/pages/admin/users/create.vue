<template>
    <form @submit.prevent="createUsers">
        <a-card title="Tạo mới tài khoản" style="width: 100%;">
            <div class="row">
                <div class="col-12 col-sm-4">
                    <div class="row">

                        <div class="col-12 d-flex justify-content-center mb-3">
                            <a-avatar shape="square" :size="200">
                                <template #icon>
                                    <img src="../../../assets/users.jpg" alt="Avatar">
                                </template>
                            </a-avatar>
                        </div>

                        <div class="col-12 d-flex justify-content-center">
                            <a-button type="primary">
                                <font-awesome-icon :icon="['fas', 'plus']" class="me-2" />
                                <span>
                                    Chọn ảnh
                                </span>
                            </a-button>
                        </div>
                    </div>
                </div>

                <div class="col-12 col-sm-8">
                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span>Tình trạng :</span>
                            </label>
                        </div>

                        <div class="col-12 col-sm-5">
                            <a-select show-search placeholder="Tình trạng" style="width: 100%" :options="users_status"
                                :filter-option="filterOption" allow-clear v-model:value="status_id">
                            </a-select>
                        </div>
                    </div>

                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span>Tên tài khoản :</span>
                            </label>
                        </div>

                        <div class="col-12 col-sm-5">
                            <a-input placeholder="Tên tài khoản" allow-clear v-model:value="username" />
                        </div>
                    </div>

                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span>Họ và tên :</span>
                            </label>
                        </div>

                        <div class="col-12 col-sm-5">
                            <a-input placeholder="Họ và tên" allow-clear v-model:value="name" />
                        </div>
                    </div>

                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span>Email :</span>
                            </label>
                        </div>

                        <div class="col-12 col-sm-5">
                            <a-input placeholder="Email" allow-clear v-model:value="email" />
                        </div>
                    </div>

                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span>Phòng ban :</span>
                            </label>
                        </div>

                        <div class="col-12 col-sm-5">
                            <a-select show-search placeholder="Phòng ban" style="width: 100%" :options="departments"
                                :filter-option="filterOption" allow-clear v-model:value="department_id">
                            </a-select>
                        </div>
                    </div>

                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span>Mật khẩu :</span>
                            </label>
                        </div>

                        <div class="col-12 col-sm-5">
                            <a-input-password placeholder="Mật khẩu" allow-clear v-model:value="password" />
                        </div>
                    </div>

                    <div class="row mb-3">
                        <div class="col-12 col-sm-3 text-start text-sm-end">
                            <label>
                                <span class="text-danger me-1">*</span>
                                <span>Xác nhận mật khẩu :</span>
                            </label>
                        </div>

                        <div class="col-12 col-sm-5">
                            <a-input-password placeholder="Xác nhận mật khẩu" allow-clear
                                v-model:value="password_confirmation" />
                        </div>
                    </div>
                </div>
            </div>

            <div class="row">
                <div class="col-12 d-grid d-sm-flex justify-content-sm-end mx-auto">
                    <a-button class="me-0 me-sm-2 mb-3 mb-sm-0">
                        <router-link :to="{ name: 'admin-users' }">Hủy</router-link>
                    </a-button>

                    <a-button type="primary" html-type="submit">
                        <span>Lưu</span>
                    </a-button>
                </div>
            </div>

        </a-card>
    </form>
</template>

<script>
import { defineComponent, ref, reactive, toRefs } from 'vue';
import { useMenu } from '../../../stores/use-menu';
import axios from 'axios';

export default defineComponent({
    setup() {
        useMenu().onSelectedKeys(['admin-users']);

        const users_status = ref([]);
        const departments = ref([]);
        const users = reactive({
            username: "",
            name: "",
            email: "",
            password: "",
            password_confirmation: "",
            department_id: [],
            status_id: []
        });

        const getUsersCreate = () => {
            axios.get("http://127.0.0.1:8000/api/users/create")
                .then((response) => {
                    users_status.value = response.data.users_status;
                    departments.value = response.data.departments;
                })
                .catch((error) => {
                    console.log(response.data);
                });
        };

        const filterOption = (input, option) => {
            return option.label.toLowerCase().indexOf(input.toLowerCase()) >= 0;
        };

        const createUsers = () => {
            axios.post("http://127.0.0.1:8000/api/users", users)
                .then((response) => {
                    console.log(response)
                })
                .catch((error) => {
                    console.log(error)
                });
        }

        getUsersCreate();

        return {
            users_status,
            departments,
            ...toRefs(users),
            filterOption,
            createUsers
        }
    },
});
</script>