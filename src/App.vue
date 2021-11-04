<template>
  <div class="masonry">
    <div class="item" :key="i.id" v-for="i in data">
      <img :src="i.img">
      <span class="title">{{i.value}}</span>
    </div>
  </div>
</template>

<script>
import data from "./data.json";
export default {
  data() {
    return {
      data
    };
  }
};
</script>

<style scoped>
  .masonry {
    column-count: 3;
    column-gap: 10px;
    padding: 10px;
  }
  .item {
    break-inside: avoid;
    border: 1px solid #999;
    margin-bottom: 10px;
  }
  img {
    width: 100%;
    vertical-align: middle;
  }
  .title {
    display: block;
    margin-left: 5px;
  }
</style>
