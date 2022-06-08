<template>
  <div class="goods-container">
    <!-- 左侧图片 -->
    <div class="thumb">
      <div class="custom-control custom-checkbox">
        <!-- 复选框 -->
        <input
          type="checkbox"
          class="custom-control-input"
          :id="'cb' + this.id"
          :checked="goods_status"
          @change="toStatus"
        />
        <label class="custom-control-label" :for="'cb' + this.id">
          <!-- 商品的缩略图 -->
          <img src="../../assets/logo.png" alt="" />
        </label>
      </div>
    </div>
    <!-- 右侧信息区域 -->
    <div class="goods-info">
      <!-- 商品标题 -->
      <h6 class="goods-title">{{ title }}</h6>
      <div class="goods-info-bottom">
        <!-- 商品价格 -->
        <span class="goods-price">￥{{ price }}</span>
        <!-- 商品的数量 -->
      </div>
    </div>
    <Count :count="num" :id="id"></Count>
  </div>
</template>

<script>
import Count from "@/components/Counter/Counter.vue";
export default {
  props: {
    id: {
      require: true,
      type: Number,
    },
    num: {
      type: Number,
      default: 0,
    },
    goods_status: {
      type: Boolean,
      require: true,
    },
    title: {
      type: String,
      require: true,
    },
    price: {
      type: Number,
      require: true,
    },
  },
  methods: {
    toStatus(e) {
      const newStatus = e.target.checked;
      const obj = { id: this.id, status: newStatus };
      this.$emit("status", obj);
    },
  },
  components: {
    Count,
  },
};
</script>

<style lang="less" scoped>
.goods-container {
  + .goods-container {
    border-top: 1px solid #efefef;
  }
  padding: 10px;
  display: flex;
  .thumb {
    display: flex;
    align-items: center;
    img {
      width: 100px;
      height: 100px;
      margin: 0 10px;
    }
  }

  .goods-info {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex: 1;
    .goods-title {
      font-weight: bold;
      font-size: 12px;
    }
    .goods-info-bottom {
      display: flex;
      justify-content: space-between;
      .goods-price {
        font-weight: bold;
        color: red;
        font-size: 13px;
      }
    }
  }
}
</style>
