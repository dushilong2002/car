<template>
  <div class="app-container">
    <Header></Header>
    <Goods
      v-for="item in list"
      :key="item.id"
      :goods_status="item.goods_state"
      :title="item.goods_name"
      :price="item.goods_price"
      :id="item.id"
      :num="item.goods_count"
      @status="newStatus"
    ></Goods>
    <Footer :all="Select" @full="isfull" :sum="sum" :num="num"></Footer>
  </div>
</template>

<script>
import Header from "@/components/Header/Header.vue";
import axios from "axios";
import Goods from "@/components/Goods/Goods.vue";
import Footer from "@/components/Footer/Footer.vue";
import bus from "@/components/enentBus.js";

export default {
  created() {
    this.initCarList();
    bus.$on("share", (val) => {
      this.list.some((item) => {
        if (item.id === val.id) {
          item.goods_count = val.count;
          return true;
        }
      });
    });
  },
  data() {
    return {
      list: [],
    };
  },
  methods: {
    async initCarList() {
      const { data: res } = await axios.get("https://www.escook.cn/api/cart");
      console.log(res);
      this.list = res.list;
    },
    newStatus(val) {
      this.list.some((item) => {
        if (item.id === val.id) {
          item.goods_state = val.status;
          return true;
        }
      });
    },
    isfull(val) {
      if (val) {
        this.list.forEach((item) => {
          item.goods_state = val;
        });
      }
    },
  },
  computed: {
    Select() {
      return this.list.every((item) => item.goods_state);
    },
    sum() {
      return this.list
        .filter((item) => item.goods_state)
        .reduce(
          (total, item) => (total += item.goods_count * item.goods_price),
          0
        );
    },
    num() {
      return this.list
        .filter((item) => item.goods_state)
        .reduce((total, item) => (total += item.goods_count), 0);
    },
  },

  components: {
    Header,
    Goods,
    Footer,
  },
};
</script>

<style lang="less" scoped>
.app-container {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
