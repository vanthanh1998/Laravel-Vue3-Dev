<template>
  <form @submit.prevent="createUsers()" action="">
    <a-card title="Tạo mới Tài khoản" style="width: 100%">
      <div class="row mb-3">
        <div class="col-12 col-sm-4 mb-3">
          <div class="row">
            <div class="col-12 d-flex justify-content-center mb-3">
              <a-avatar shape="square" :size="200">
                <template #icon>
                  <img src="../../../assets/users.jpg" alt="Avatar" />
                </template>
              </a-avatar>
            </div>

            <div class="col-12 d-flex justify-content-center">
              <a-button type="primary">
                <i class="fa-solid fa-plus me-2"></i>
                <span>Chọn ảnh</span>
              </a-button>
            </div>
          </div>
        </div>

        <div class="col-12 col-sm-8">
          <div class="row mb-3">
            <div class="col-12 col-sm-3 text-start text-sm-end">
              <label>
                <span class="text-danger me-1">*</span>
                <span
                  :class="{
                    'text-danger': errors.status_id,
                  }"
                  >Tình trạng:</span
                >
              </label>
            </div>

            <div class="col-12 col-sm-5">
              <a-select
                show-search
                placeholder="Tình trạng"
                style="width: 100%"
                :options="users_status"
                :filter-option="filterOption"
                allow-clear
                v-model:value="users.status_id"
                :class="{
                  'select-danger': errors.status_id,
                }"
              ></a-select>
              <div class="w-100"></div>
              <small v-if="errors.status_id" class="text-danger">{{
                errors.status_id[0]
              }}</small>
            </div>
          </div>

          <div class="row mb-3">
            <div class="col-12 col-sm-3 text-start text-sm-end">
              <label>
                <span class="text-danger me-1">*</span>
                <span
                  :class="{
                    'text-danger': errors.username,
                  }"
                  >Tên Tài khoản:</span
                >
              </label>
            </div>

            <div class="col-12 col-sm-5">
              <a-input
                placeholder="Tên Tài khoản"
                allow-clear
                v-model:value="users.username"
                :class="{
                  'select-danger': errors.username,
                }"
              />
              <div class="w-100"></div>
              <small v-if="errors.username" class="text-danger">{{
                errors.username[0]
              }}</small>
            </div>
          </div>

          <div class="row mb-3">
            <div class="col-12 col-sm-3 text-start text-sm-end">
              <label>
                <span class="text-danger me-1">*</span>
                <span
                  :class="{
                    'text-danger': errors.status_id,
                  }"
                  >Họ và Tên:</span
                >
              </label>
            </div>

            <div class="col-12 col-sm-5">
              <a-input
                placeholder="Họ và Tên"
                allow-clear
                v-model:value="users.name"
                :class="{
                  'select-danger': errors.name,
                }"
              />
              <div class="w-100"></div>
              <small v-if="errors.name" class="text-danger">{{
                errors.name[0]
              }}</small>
            </div>
          </div>

          <div class="row mb-3">
            <div class="col-12 col-sm-3 text-start text-sm-end">
              <label>
                <span class="text-danger me-1">*</span>
                <span
                  :class="{
                    'text-danger': errors.email,
                  }"
                  >Email:</span
                >
              </label>
            </div>

            <div class="col-12 col-sm-5">
              <a-input
                placeholder="Email"
                allow-clear
                v-model:value="users.email"
                :class="{
                  'select-danger': errors.email,
                }"
              />
              <div class="w-100"></div>
              <small v-if="errors.email" class="text-danger">{{
                errors.email[0]
              }}</small>
            </div>
          </div>

          <div class="row mb-3">
            <div class="col-12 col-sm-3 text-start text-sm-end">
              <label>
                <span class="text-danger me-1">*</span>
                <span
                  :class="{
                    'text-danger': errors.department_id,
                  }"
                  >Phòng ban:</span
                >
              </label>
            </div>

            <div class="col-12 col-sm-5">
              <a-select
                show-search
                placeholder="Phòng ban"
                style="width: 100%"
                :options="departments"
                :filter-option="filterOption"
                allow-clear
                v-model:value="users.department_id"
                :class="{
                  'select-danger': errors.department_id,
                }"
              ></a-select>
              <div class="w-100"></div>
              <small v-if="errors.department_id" class="text-danger">{{
                errors.department_id[0]
              }}</small>
            </div>
          </div>

          <div class="row mb-3">
            <div class="col-12 col-sm-3 text-start text-sm-end">
              <label>
                <span class="text-danger me-1">*</span>
                <span
                  :class="{
                    'text-danger': errors.password,
                  }"
                  >Mật khẩu:</span
                >
              </label>
            </div>

            <div class="col-12 col-sm-5">
              <a-input-password
                placeholder="Mật khẩu"
                allow-clear
                v-model:value="users.password"
                :class="{
                  'select-danger': errors.password,
                }"
              />
              <div class="w-100"></div>
              <small v-if="errors.password" class="text-danger">{{
                errors.password[0]
              }}</small>
            </div>
          </div>

          <div class="row mb-3">
            <div class="col-12 col-sm-3 text-start text-sm-end">
              <label>
                <span class="text-danger me-1">*</span>
                <span>Xác nhận mật khẩu:</span>
              </label>
            </div>

            <div class="col-12 col-sm-5">
              <a-input-password
                placeholder="Xác nhận mật khẩu"
                allow-clear
                v-model:value="users.password_confirmation"
              />
            </div>
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col-12 d-grid d-sm-flex justify-content-sm-end mx-auto">
          <a-button class="me-0 me-sm-2 mb-3 mb-sm-0">
            <router-link :to="{ name: 'admin-users' }">
              <span>Hủy</span>
            </router-link>
          </a-button>

          <!-- htmlType: thuộc tính của antdv -->
          <a-button type="primary" htmlType="submit">
            <span>Lưu</span>
          </a-button>
        </div>
      </div>
    </a-card>
  </form>
</template>

<script setup>
import { onMounted, reactive, ref } from "vue";
import { useMenu } from "../../../stores/use-menu.js";
import { message } from "ant-design-vue";
import { useRouter } from "vue-router";

useMenu().onSelectedKeys(["admin-users"]);

const users_status = ref([]);
const departments = ref([]);

const router = useRouter();
const users = reactive({
  username: "",
  name: "",
  email: "",
  password: "",
  password_confirmation: "",
  department_id: [],
  status_id: [],
});

const errors = ref({});

onMounted(() => {
  getUsersCreate();
});

async function getUsersCreate() {
  try {
    const response = await axios.get(
      `${import.meta.env.VITE_API_BASE_URL}/api/users/create`
    );

    users_status.value = response.data.users_status;
    departments.value = response.data.departments;
  } catch (error) {
    console.error(error);
  }
}

function filterOption(input, option) {
  return option.label.toLowerCase().indexOf(input.toLowerCase()) >= 0;
}

async function createUsers() {
  try {
    const response = await axios.post(
      `${import.meta.env.VITE_API_BASE_URL}/api/users`,
      users
    );
    if (response.status == 200) {
      message.success("Tạo mới thành công");
      router.push({ name: "admin-users" });
    }
  } catch (error) {
    errors.value = error.response.data.errors;
  }
}
</script>

<style>
.select-danger {
  border: 1px solid red;
}

.input-danger {
  border-color: red;
}
</style>
