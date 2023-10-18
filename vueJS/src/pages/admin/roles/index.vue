<template>
  <div>
    <p>page roles</p>
  </div>
</template>

<script setup>
import { useMenu } from "../../../stores/use-menu";

useMenu().onSelectedKeys(["admin-roles"]);
</script>
