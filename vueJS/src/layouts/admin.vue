<template>
  <TheHeader />
  <div class="container-fluid mt-3">
    <div class="row">
      <div class="col-sm-3">
        <a-list bordered style="width: 100%">
          <TheMenu />
          <template #header>
            <div>BẢNG ĐIỀU KHIỂN</div>
          </template>
        </a-list>
      </div>
      <div class="col-sm-9">
        <router-view></router-view>
      </div>
    </div>
  </div>
</template>

<script setup>
import TheHeader from "../components/TheHeader.vue";
import TheMenu from "../components/TheMenu.vue";
</script>
