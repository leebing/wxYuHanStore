<!--收藏or历史足迹列表-->
<template name="cart-goods-list">
  <view class="goodsList">
    <repeat for="{{list}}" key="index" index="index" item="item">
      <view class="list_box">
        <swipeDelete :swipeData="item" @delItem.user="handleDelItem">
        <navigator class="item_content" url="/pages/goods_detail?id={{item.goodsId}}">
          <view class="goods-info">
            <view class="img-box">
              <image src="{{item.thumLogo}}" class="img" />
            </view>
            <view class="text-box">
              <view class="goods-title">{{item.name}}</view>
              <view class="goods-price">¥ {{item.price}}</view>
            </view>
          </view>
        </navigator>
        </swipeDelete>
      </view>
    </repeat>
  </view>
</template>
<script>
import wepy from 'wepy';
import {
  SYSTEM_INFO,
  USER_SPECICAL_INFO
} from '../utils/constant';
import tip from '../utils/tip'
import api from '../api/api';
import SwipeDelete from './common/wepy-swipe-delete'
export default class CollecntionList extends wepy.component {
  props = {
    type : {
      default: 0
    },
    list: {
      type: Object,
      default: []
    }
  }
  components = {
    swipeDelete: SwipeDelete
  }

  onLoad() {
    let that = this;
    console.log(that.list)

  }
  computed = {

  }

  //商品取消收藏
  async goodsUnFavorite(goodsId) {
    let that = this;
    let userSpecialInfo = wepy.getStorageSync(USER_SPECICAL_INFO) || {};
    let openId = userSpecialInfo.openid;
    const json = await api.goodsUnFavorite({
      query: {
        openId: openId,
        goodsId: goodsId
      }
    });
    if (json.data.code == 0) {
      console.log("===========商品取消收藏成功=========")
      //tip.toast("取消收藏成功");
      let retList = [];
      for (var i = 0; i < this.list.length; i++) {
        if (this.list[i].goodsId == goodsId) {
          continue;
        } else {
          retList.push(this.list[i]);
        }
      }
      this.list = retList;
    } else {
      tip.error(json.data.msg)
    }
    that.$apply();
  }

  //商品取消收藏
  async delUserBrowser(goodsId) {
    let that = this;
    let userSpecialInfo = wepy.getStorageSync(USER_SPECICAL_INFO) || {};
    let openId = userSpecialInfo.openid;
    const json = await api.delUserBrowser({
      query: {
        openId: openId,
        goodsId: goodsId
      }
    });
    if (json.data.code == 0) {
      //tip.toast("取消收藏成功");
      let retList = [];
      for (var i = 0; i < this.list.length; i++) {
        if (this.list[i].goodsId == goodsId) {
          continue;
        } else {
          retList.push(this.list[i]);
        }
      }
      this.list = retList;
    } else {
      tip.error(json.data.msg)
    }
    that.$apply();
  }

  methods = {
    handleDelItem(itemData) {
      console.log(itemData)
      let objType = itemData.type;
      if (objType==1) {
        this.delUserBrowser(itemData.goodsId);
      } else if (objType==2) {
        this.goodsUnFavorite(itemData.goodsId);
      }
    },
    refreshList(val){
       if (val==undefined) return;
       console.log("val.....",val);
        this.list = val;
        this.$apply();
    }
  }
  events = {

  }
}

</script>
<style lang="less">
.goodsList {
  padding-top: 15rpx;
}

.goods-info {
  border-bottom: 1px solid #eee;
  display: flex;
  justify-content: space-between;
  padding: 15rpx 21rpx;
  box-sizing: border-box;
}

.goods-info .img-box {
  width: 175rpx;
  height: 175rpx;
  overflow: hidden;
  margin-right: 20rpx;
  background-color: #d8d8d8;
}

.goods-info .text-box {
  width: 440rpx;
  position: relative;
}

.goods-info .text-box .goods-title {
  font-size: 32rpx;
  color: #414141;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
  padding: 10rpx 20rpx 5rpx 0;
}

.goods-info .text-box .goods-price {
  font-size: 30rpx;
  color: #ed601b;
  padding-top: 30rpx;
}

.goods-info .img-box .img {
  width: 175rpx;
  height: 175rpx;
}

.list_box {
  height: 200rpx;
}

</style>
