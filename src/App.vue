<template>
  <div class="masonry" ref="parent">
    <div class="item non-vis" :key="i.id" v-for="i in data">
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
  },
  mounted() {
    this.setPos(this.$refs.parent)
  },
  methods: {
    async setPos(parentNode) {
      const children = parentNode.children;
      let heightLeft = 0, heightRight = 0;
      const gap = 10;
      const align = async (childNode, where) => {
        // 获取到父盒子实际宽度
        const imgInChild = childNode.querySelector('img');
        await this.imgLoaded(imgInChild);
        const childHeight = parseFloat(window.getComputedStyle(childNode).height);
        if (where === 'left') {
          heightLeft += (childHeight + gap);
          childNode.classList.add('float-left')
        } else {
          heightRight += (childHeight + gap);
          childNode.classList.add('float-right')
        }
        childNode.classList.remove('non-vis')
      };
      for (let child of children) {
        heightLeft <= heightRight
          ? await align(child, 'left')
          : await align(child, 'right')
      }
    },
    async imgLoaded(imgNode) {
      if (imgNode.complete) {
        return Promise.resolve();
      } else {
        return new Promise(resolve => {
          imgNode.addEventListener('load', () => {
            resolve()
          })
        })
      }
    }
  }
};
</script>

<style>
.masonry {
  overflow: hidden;
  padding: 10px;
}
.item {
  width: 45%;
  border: 1px solid #999;
  margin-bottom: 10px;
  overflow: hidden;
}
.float-left {
  float: left;
}
.float-right {
  float: right;
}
.non-vis {
  visibility: hidden;
}
img {
  width: 100%;
  /*height: 250px;*/
  vertical-align: middle;
}
.title {
  display: block;
  margin-left: 5px;
}
</style>
