<template><section class="demo-quantity"><h1 class="demo-title">Quantity 数量选择</h1><example-block title="基础用法">
                <van-quantity v-model="quantity1"></van-quantity>
<p class="curr-quantity">当前值：{{ quantity1 }}</p>

              </example-block><example-block title="禁用Quantity">
                <van-quantity v-model="quantity1" disabled></van-quantity>

              </example-block><example-block title="高级用法">
                <van-quantity v-model="quantity2" min="5" max="40" step="2" default-value="9"></van-quantity>
<p class="curr-quantity">当前值：{{ quantity2 || 9 }}</p>

              </example-block></section></template>
<style>
@component-namespace demo {
  @b quantity {
    .van-quantity {
      margin-left: 15px;
    }

    .curr-quantity {
      margin: 15px;
    }
  }
}
</style>
<script>
import Vue from "vue";import ExampleBlock from "components/example-block";Vue.component("example-block", ExampleBlock);
export default {
  data() {
    return {
      quantity1: 1,
      quantity2: null,
    };
  }
};
</script>