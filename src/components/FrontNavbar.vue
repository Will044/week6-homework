/* eslint-disable quotes */
<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <router-link class="navbar-brand" to="/">W重車高級量販店</router-link>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link class="nav-link" to="/">首頁</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/products">產品列表</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/cart">購物車</router-link>
          </li>
        </ul>
      </div>
      <button type="button" class="btn btn-primary">
        結帳
        <span class="badge rounded-pill bg-danger">{{
          cartData.carts.length
        }}</span>
      </button>
    </div>
  </nav>
</template>

<script>
// eslint-disable-next-line quotes
import emitter from "@/libs/emitter";

export default {
  data() {
    return {
      cartData: {
        carts: [],
      },
    };
  },
  methods: {
    getCart() {
      this.$http
        .get(`${process.env.VUE_APP_API}/api/${process.env.VUE_APP_PATH}/cart`)
        .then((res) => {
          this.cartData = res.data.data;
        });
    },
  },
  mounted() {
    this.getCart();
    // eslint-disable-next-line quotes
    emitter.on("get-cart", () => {
      this.getCart();
    });
  },
};
</script>
