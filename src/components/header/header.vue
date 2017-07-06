<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avater">
        <img width="64" height="64" :src="seller.avatar" alt="">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name1">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count" @click="showDetail">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>

    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>

    <div class="background">
      <img width="100%" height="100%" :src="seller.avatar" alt="">
    </div>

    <transition name="fade">
      <div v-show="detailShow" class="detail">

        <div class="detail-wrapper clearfix">
          <div class="detail-main">
            <h1 class="name">{{seller.name}}</h1>

            <div class="star-wrapper">
              <star :size="48" :score="seller.score"></star>
            </div>

            <div class="title">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>

            <ul v-if="seller.supports" class="supports">
              <li class="support-item" v-for="(item, index) in seller.supports">
                <span class="icon" :class="classMap[seller.supports[index].type]"></span>
                <span class="text">{{seller.supports[index].description}}</span>
              </li>
            </ul>

            <div class="title">
              <div class="line"></div>
              <div class="text">商家公告</div>
              <div class="line"></div>
            </div>

            <div class="bulletin">
              <p class="content">{{seller.bulletin}}</p>
            </div>

          </div>
        </div>

        <div class="detail-close">
          <i class="icon-close" @click="hideDetail"></i>
        </div>

      </div>
    </transition>


  </div>
</template>

<script type="text/ecmascript-6">
  import star from '../star/star'

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data() {
      return {
        detailShow: false
      }
    },
    methods: {
      showDetail() {
        this.detailShow = true
      },
      hideDetail() {
        this.detailShow = false
      }
    },
    created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    },
    components: {
      star
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import '../../common/stylus/mixin'

  .header {
    position: relative
    color: #fff
    background: rgba(7, 17, 27, 0.5)
    overflow: hidden
  }

  .header .content-wrapper {
    position: relative
    padding: 24px 12px 18px 24px
    font-size: 0px
  }

  .content-wrapper .avater {
    display: inline-block
    vertical-align: top
  }

  .avater img {
    border-radius: 2px
  }

  .content-wrapper .content {
    display: inline-block
    font-size: 14px
    margin-left: 14px
  }

  .content .title {
    margin: 2px 0 8px 0
  }

  .title .brand {
    display: inline-block
    vertical-align: top
    width: 30px
    height: 18px
    bg-image('brand')
    background-size: 30px 18px
    background-repeat: no-repeat
  }

  .title .name1 {
    margin-left: 6px
    font-size: 16px
    line-height: 18px
    font-weight: bold
  }

  .content .description {
    margin-bottom: 10px
    line-height: 12px
    font-size: 12px
  }

  .content .support {
    font-size: 12px
    line-height: 12px
  }

  .support .icon {
    display: inline-block
    width: 12px
    height: 12px
    margin-right: 4px
    background-size: 12px 12px
    background-repeat: no-repeat
    vertical-align: top
  }

  .support .decrease {
    bg-image('decrease_1')
    vertical-align: top
  }

  .support .discount {
    bg-image('discount_1')
  }

  .support .guarantee {
    bg-image('guarantee_1')
  }

  .support .invoice {
    bg-image('invoice_1')
  }

  .support special {
    bg-image('special_1')
  }

  .support .text {
    display: inline-block
    height: 12px
    line-height 12px
    font-size 12px
  }

  .content-wrapper .support-count {
    position: absolute
    right: 12px
    bottom: 18px
    padding: 0 8px
    height: 24px
    line-height: 24px
    border-radius: 14px
    background: rgba(0, 0, 0, 0.2)
    text-align: center
  }

  .support-count .count {
    vertical-align: top
    font-size: 10px
  }

  .support-count .icon-keyboard_arrow_right {
    margin-left: 2px
    line-height: 24px
    font-size: 10px
  }

  .header .bulletin-wrapper {
    position: relative
    height: 28px
    line-height: 28px
    padding: 0 22px 0 12px
    /*background #adadad*/
    white-space: nowrap
    overflow: hidden
    text-overflow: ellipsis
    background: rgba(7, 17, 27, 0.2)
  }

  .bulletin-wrapper .bulletin-title {
    display: inline-block
    width: 22px
    height: 14px
    vertical-align: top
    margin-top: 7px
    bg-image('bulletin')
    background-size: 22px 12px
    background-repeat: no-repeat
  }

  .bulletin-wrapper .bulletin-text {
    vertical-align: top
    margin: 0 4px
    font-size: 10px
  }

  .bulletin-wrapper .icon-keyboard_arrow_right {
    position: absolute
    right: 12px
    top: 10px
    font-size: 10px
  }

  .header .background {
    position: absolute
    top: 0
    left: 0
    width: 100%
    height: 100%
    z-index: -1;
    filter: blur(10px) /*模糊滤镜*/
  }

  .header .detail {
    position: fixed
    z-index: 100
    top: 0
    left: 0
    width: 100%
    height: 100%
    overflow: auto
    transition: all .5s
    background: rgba(7, 17, 27, 0.8)
  }

  .fade-enter-active, .fade-leave{
    opacity: 1;
    background: rgba(7, 17, 27, 0.8)
  }
  .fade-enter, .fade-leave-active {
    opacity: 0
    background: rgba(7, 17, 27, 0)
  }

  .detail .detail-wrapper {
    width: 100%
    min-height: 100%
  }

  .detail-wrapper .detail-main {
    margin-top: 64px
    padding-bottom: 64px
  }

  .detail-main .name {
    line-height: 16px
    text-align: center
    font-size: 16px
    font-weight: 700
  }

  .detail .detail-close {
    position: relative
    width: 32px
    height: 32px
    margin: -64px auto 0 auto
    clear: both
    font-size: 32px
  }

  .detail-main .star-wrapper {
    margin-top: 18px
    padding: 2px 0
    text-align: center
  }

  .detail-main .title {
    display: flex
    width: 80%
    margin: 28px auto
  }

  .title .line {
    flex: 1
    position: relative
    top: -6px
    border-bottom: 1px solid rgba(255, 255, 255, 0.2)
  }

  .title .text {
    padding: 0 12px
    font-weight: 700
    font-size: 14px
  }

  .detail-main .supports {
    width: 80%
    margin: 0 auto
  }

  .supports .support-item {
    padding: 0 12px
    margin-bottom: 12px
    font-size: 0px
  }

  .supports:last-child {
    margin-bottom: 0
  }

  .supports .icon {
    display: inline-block
    width: 16px
    height: 16px
    vertical-align: top
    margin-right: 6px
    background-size: 16px 16px
    background-repeat: no-repeat
  }
  .supports .decrease {
    bg-image('decrease_2')
  }

  .supports .discount {
    bg-image('discount_2')
  }

  .supports .guarantee {
    bg-image('guarantee_2')
  }

  .supports .invoice {
    bg-image('invoice_2')
  }

  .supports .special {
    bg-image('special_2')
  }

  .supports .text {
    line-height: 16px
    font-size: 12px
  }

  .detail-main .bulletin {
    width: 80%
    margin: 0 auto
  }

  .bulletin .content {
    padding: 0 12px
    line-height: 24px
    font-size: 12px
  }
</style>
