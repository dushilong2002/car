<template>
  <div
    class="number-container d-flex justify-content-center align-items-center"
  >
    <!-- 减 1 的按钮 -->
    <button type="button" class="btn btn-light btn-sm" @click="sub">-</button>
    <!-- 购买的数量 -->
    <span class="number-box">{{ count }}</span>
    <!-- 加 1 的按钮 -->
    <button type="button" class="btn btn-light btn-sm" @click="add">+</button>
  </div>
</template>

<script>
import bus from "@/components/enentBus.js";
export default {
  props: {
    id: {
      type: Number,
    },
    count: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    add() {
      const num = this.count + 1;
      const obj = { id: this.id, count: num };
      bus.$emit("share", obj);
    },
    sub() {
      const num = this.count - 1;
      if (num <= 0) return;
      const obj = { id: this.id, count: num };
      bus.$emit("share", obj);
    },
  },
};
</script>

<style lang="less" scoped>
.number-box {
  min-width: 30px;
  text-align: center;
  margin: 0 5px;
  font-size: 12px;
}

.btn-sm {
  width: 30px;
}
</style>
