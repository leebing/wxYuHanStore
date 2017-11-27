<template>
  <view class="job_request">
    <shopCart></shopCart>
  </view>
</template>
<script>
import wepy from 'wepy';
import ShopCart from '../components/job_request'
export default class shopCart extends wepy.page {
  config = {
    navigationBarTitleText: '我的工作',
  }
  components = {
    shopCart: ShopCart
  }
  data = {

  }

  onLoad() {
  }
  onShow() {
    this.$invoke('shopCart', 'getCartListMethod');
  }
  computed = {

  }
  methods = {

  }
  events = {

  }
}

</script>
<style lang="less">
.job_request {
  background: #f7f7f7;
}

</style>
