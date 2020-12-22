<template>
  <div class="tab-bar-item" @click="itemClick">
    <slot v-if="!isActive" name="item-icon"></slot>
    <div v-else><slot name="item-icon-active"></slot></div>
    <div :style="activeStyle"><slot name="item-text"></slot></div>
  </div>
</template>

<script>
export default {
  name: "TabBarItem",
  props: {
    link: String,
    activeColor: {
      type: String,
      default: "red"
    }
  },
  data() {
    return {
      // isActive:true
    };
  },
  computed: {
    isActive() {
      // this.link 可能是/home 然后现在激活的route路径是不是/home 如果不是就返回-1 是就true
      return this.$route.path.indexOf(this.link) !== -1;
    },
    activeStyle() {
      return this.isActive?{color:this.activeColor}:{};
    }
  },
  methods: {
    itemClick() {
      this.$router.replace(this.link);
    }
  }
};
</script>

<style scoped>
.tab-bar-item {
  flex: 1;
  text-align: center;
  height: 49px;
  font-size: 14px;
}

.tab-bar-item img {
  width: 24px;
  height: 24px;
  margin-top: 3px;
  /* 解决图片空隙 */
  vertical-align: middle;
  margin-bottom: 2px;
}
</style>