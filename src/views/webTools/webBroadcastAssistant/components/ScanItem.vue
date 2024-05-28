<template>
  <div class="container">
    <div class="item-left">
      <div>Device Name: {{ props.name }}</div>
      <div>Device Addr: {{ props.addr }}</div>
    </div>
    <div class="item-right">
      <el-button>连接</el-button>
    </div>
  </div>
</template>

<script lang="ts" setup>
interface Props {
  name: string;
  addr: string;
}
const props = withDefaults(defineProps<Props>(), {
  name: "Auracast",
  addr: "AA:BB:CC:DD:EE:FF"
});
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  margin: 10px;
  border: 2px solid pink;
}
.container .item-left {
  flex-direction: column;
}
</style>
