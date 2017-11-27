<!--积分规则-->
<template>
  <view class="jf_rule">
    <view class="title tc">佣金规则</view>
    <!--<view class="jf_jz_title tc">积分价值</view>-->
    <view class="jf_content">
      <view class="sec_title">1.推荐佣金计算方式 </view>
      <view class="jf_ins">根据每个被推荐者实际工作时间，在被推荐者获取工资后，结算推荐者的推荐佣金。</view>
    </view>
    <view class="jf_content">
      <view class="sec_title">2.管理佣金计算方式 </view>
      <view class="jf_ins">按照实际管理人数、管理的工作量（工时）在结算工资后结算管理佣金。</view>
    </view>
    <view class="jf_content">
      <view class="sec_title">3.佣金提取规则 </view>
      <view class="jf_ins">可按10元的整倍数提取佣金（如109.9元可提取100元，9.9元先累计在平台，待满整后提取。</view>
    </view>
    <!--<view class="jf_content">
      <view class="sec_title">积分社区的价值</view>
      <view class="jf_ins">小e们听过各种社区互动获得的积分可以用于提升小嗨的等级，等级越高开启的社区特权越多。</view>
    </view>-->
  </view>
</template>
<script>
import wepy from 'wepy'

export default class PointsRule extends wepy.component {
  data = {

  }

  events = {
    // 'index-broadcast': (...args) => {
    //   let $event = args[args.length - 1]
    //   console.log(`${this.$name} receive ${$event.name} from ${$event.source.name}`)
    // }
  }

  methods = {

  }

  onLoad() {}
}

</script>
<style lang="less">
.jf_rule {
  border-top: 1px solid #efefef;
  background: #fff;
  padding: 33px 20rpx;
  margin-top: 10rpx;
  .title {
    font-size: 36rpx;
  }
  .jf_jz_title {
    color: #9999ff;
    font-size: 30rpx;
    padding-top: 56rpx;
    display: block;
  }
  .jf_content {
    text-align: left;
    font-size: 30rpx;
    .sec_title {
      color: #666;
      padding-top: 40rpx;
    }
    .jf_ins {
      color: #999;
      padding-top: 30rpx;
    }
  }
}

</style>
