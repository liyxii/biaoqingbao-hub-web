<script lang="ts" setup>
import { NImage } from "naive-ui";
import axios from "axios";
import { ref } from "vue";
const baseURL = "http://127.0.0.1:10001";
const imgdata = ref();
interface imgdata {
  url: string;
  name: string;
}
(async () => {
  const res = await axios.get(`${baseURL}/getimg`);
  imgdata.value = res.data as imgdata;
})();
let imgv = ref(250);
if (window.innerWidth < 1020) {
  imgv.value = 100;
}
</script>

<template>
  <div class="app">
    <n-image-group>
      <n-space>
        <div class="imgcard" v-for="item in imgdata">
          <div class="img">
            <n-image :src="item.url" :width="imgv" lazy object-fit="contain" />
          </div>
          <p>{{ item.name }}</p>
        </div></n-space
      >
    </n-image-group>
  </div>
</template>

<style lang="less" scoped>
* {
  box-sizing: border-box;
}
.app {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  justify-content: center;
  .imgcard {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-left: auto;
    margin-right: auto;
    width: 250px;
    height: 250px;
    overflow: hidden;
    border: 1px solid #ccc;
    border-radius: 3px;
    padding: 5px;
    margin-bottom: 20px;
  }
}
@media (max-width: 1020px) {
  .app {
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
    .imgcard {
      width: 100px;
      height: 100px;
    }

    .imgcard img {
      max-width: 100%;
      max-height: 100%;
      object-fit: contain;
    }
    p {
      font-size: 10px;
    }
  }
}

.imgcard img {
  width: 100%;
  height: auto;
}
</style>
