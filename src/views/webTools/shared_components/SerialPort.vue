<template>
  <div class="container">
    <el-button @click="chooseSerial" color="#626aef">选择串口</el-button>
    <el-button @click="openSerial" color="red">开启串口</el-button>
    <el-button @click="closeSerial" color="yellow" disabled>关闭串口</el-button>
    <el-button @click="sendData">发送数据</el-button>
  </div>
</template>

<script lange="ts" setup>
import { ref } from "vue";
import { ElNotification } from "element-plus";

const port = ref(null);
const reader = ref(null);
const message = ref(null);
const connected = ref(null);
const serialOptions = {
  baudRate: 115200,
  flowControl: "none",
  dataBits: 8
};

const chooseSerial = async () => {
  try {
    port.value = await navigator.serial.requestPort();
    console.log(port.value);
  } catch (error) {
    ElNotification({ title: "选择串口失败", message: "错误信息:" + error, type: "warning", duration: 2000 });
    return;
  }
  ElNotification({ title: "选择成功", message: "串口已打开", type: "success", duration: 2000 });
};

const openSerial = async () => {
  try {
    await port.value.open(serialOptions);
    reader.value = port.value.readable.getReader();
    connected.value = true;
  } catch (error) {
    ElNotification({ title: "打开串口失败", message: error, type: warning, duration: 2000 });
    return;
  }
  ElNotification({ title: "打开串口成功", message: "串口等待接收信息中", type: "success", duration: 2000 });
  readLoop();
};

const readLoop = async () => {
  try {
    while (connected.value) {
      const { value, done } = await reader.value.read();
      if (done) {
        reader.value.releaseLock();
        break;
      }
      message.value = new TextDecoder().decode(value);
    }
  } catch (error) {
    ElNotification({ title: "读取串口失败", message: `串口读取数据失败: ${error}`, type: "error", duration: 2000 });
  }
};

const closeSerial = async () => {
  try {
    await reader.value.cancel();
    await port.value.close();
    connected.value = false;
  } catch (error) {
    ElNotification({ title: "关闭串口失败", message: "请检查后重新关闭串口", type: "warning", duration: 2000 });
  }
  ElNotification({ title: "关闭串口成功", message: `已关闭串口: ${port.value.name}`, type: "success", duration: 2000 });
};

const sendData = async () => {
  console.log("sendData");
};
</script>

<style scoped>
.container {
  margin: 20px 0;
}
</style>
