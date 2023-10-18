<template>
  <form @submit.prevent="updateUsers()" action="">
    <a-card title="Cập nhật Tài khoản" style="width: 100%">
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
                v-model:value="status_id"
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
                v-model:value="username"
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
                v-model:value="name"
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
                v-model:value="email"
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
                v-model:value="department_id"
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
            <div class="col-12 col-sm-3 text-start text-sm-end"></div>

            <div class="col-12 col-sm-5">
              <a-checkbox v-model:checked="change_password"
                >Đổi mật khẩu</a-checkbox
              >
            </div>
          </div>

          <div class="row mb-3" v-if="change_password == true">
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
                v-model:value="password"
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

          <div class="row mb-3" v-if="change_password == true">
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
                v-model:value="password_confirmation"
              />
            </div>
          </div>

          <div class="row mb-3">
            <div class="col-12 col-sm-3 text-start text-sm-end">
              <label>
                <span>Lần đăng nhập gần đây:</span>
              </label>
            </div>

            <div class="col-12 col-sm-5">
              <span>{{ login_at }}</span>
            </div>
          </div>

          <div class="row mb-3">
            <div class="col-12 col-sm-3 text-start text-sm-end">
              <label>
                <span>Lần đổi mật khẩu gần đây:</span>
              </label>
            </div>

            <div class="col-12 col-sm-5">
              <span>{{ change_password_at }}</span>
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
import { onMounted, reactive, ref, toRefs } from "vue";
import { useMenu } from "../../../stores/use-menu.js";
import { message } from "ant-design-vue";
import { useRoute, useRouter } from "vue-router";
import dayjs from "dayjs";

useMenu().onSelectedKeys(["admin-users"]);

const users_status = ref([]);
const departments = ref([]);

const router = useRouter();
const route = useRoute(); // get param route index.vue
const users = reactive({
  username: "",
  name: "",
  email: "",
  password: "",
  password_confirmation: "",
  department_id: [],
  status_id: [],
  change_password: false,
  login_at: "",
  change_password_at: "",
});

const errors = ref({});

onMounted(() => {
  getUsersEdit();
});

async function getUsersEdit() {
  try {
    const response = await axios.get(
      `${import.meta.env.VITE_API_BASE_URL}/api/users/${route.params.id}/edit`
    );

    if (response.data.users) {
      users.username = response.data.users.username;
      users.name = response.data.users.name;
      users.email = response.data.users.email;
      users.department_id = response.data.users.department_id;
      users.status_id = response.data.users.status_id;

      users.login_at = response.data.users.login_at
        ? dayjs(response.data.users.login_at).format("DD/MM/YYYY - HH:mm")
        : "Chưa có lượt đăng nhập";
      users.change_password_at = response.data.users.change_password_at
        ? dayjs(response.data.users.change_password_at).format(
            "DD/MM/YYYY - HH:mm"
          )
        : "Chưa có lượt đổi mật khẩu";

      users_status.value = response.data.users_status;
      departments.value = response.data.departments;
    } else {
      router.push({ name: "notfound" });
    }
  } catch (error) {
    console.error(error);
  }
}

async function updateUsers() {
  try {
    const response = await axios.put(
      `${import.meta.env.VITE_API_BASE_URL}/api/users/${route.params.id}/edit`,
      users
    );
    if (response.status == 200) {
      message.success("Cập nhật thành công");
      router.push({ name: "admin-users" });
    }
  } catch (error) {
    errors.value = error.response.data.errors;
    console.error(error);
  }
}

function filterOption(input, option) {
  return option.label.toLowerCase().indexOf(input.toLowerCase()) >= 0;
}

const {
  username,
  name,
  email,
  password,
  password_confirmation,
  department_id,
  status_id,
  change_password,
  login_at,
  change_password_at,
} = toRefs(users);
</script>

<style>
.select-danger {
  border: 1px solid red;
}

.input-danger {
  border-color: red;
}
</style>
