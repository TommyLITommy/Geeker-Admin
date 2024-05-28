<template>
  <div class="app-title">Web Broadcast Assistant</div>
  <SerialPort />
  <div class="btns">
    <el-button type="primary">
      DISCOVER<br />
      SINKS
    </el-button>
    <el-button type="primary">
      STOP<br />
      SCANNING
    </el-button>
    <el-button type="primary">
      DISCOVER<br />
      SOURCES
    </el-button>
  </div>
  <div class="both_container">
    <div class="sink_container">
      <h1>Sink List</h1>
      <div class="filter_sink">
        <el-input v-model="filter_sink_input" style="width: 240px" placeholder="Filter Sink Device" />
      </div>
      <ScanItem v-for="(item, index) in 10" :key="index" :name="`Device: ${index}`" :addr="`AA:BB:CC:DD:EE:F${index}`"></ScanItem>
    </div>
    <div class="source_container">
      <h1>Source List</h1>
      <div class="filter_source">
        <el-input v-model="filter_source_input" style="width: 240px" placeholder="Filter Source Device" />
      </div>
      <ScanItem v-for="(item, index) in 10" :key="index"></ScanItem>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import ScanItem from "./components/ScanItem.vue";
import SerialPort from "../shared_components/SerialPort.vue";
const filter_sink_input = ref("");
const filter_source_input = ref("");
</script>

<style scoped>
.app-title {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 20px 0;
  font-size: 30px;
  font-weight: 900;
}
h1 {
  margin: 10px;

  /* border: 2px solid grey; */
}
.btns {
  display: flex;
  justify-content: space-around;
  width: 400px;
}
.both_container {
  display: flex;
  justify-content: space-between;
  width: 100%;
}
.filter_sink,
.filter_source {
  margin: 10px;

  /* border: 5px solid pink; */
}
.sink_container,
.source_container {
  width: 48%;
  margin: 10px 0;
  border: 5px solid green;
}
</style>
