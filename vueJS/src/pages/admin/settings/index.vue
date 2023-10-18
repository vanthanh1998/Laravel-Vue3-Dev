<template>
  <div>
    <p>page settings</p>
  </div>
</template>

<script setup>
import { useMenu } from "../../../stores/use-menu";

useMenu().onSelectedKeys(["admin-settings"]);
</script>
