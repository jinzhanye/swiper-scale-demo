<template>
 <div>
   <swiper ref="mySwiper"
           :options="swiperOptions"
           :auto-play="false"
           @touch-start="onTouchStart"
           @touch-move="onTouchmove"
           @touch-end="onTouchend"
   >
     <swiper-slide>Slide 1</swiper-slide>
     <swiper-slide>Slide 2</swiper-slide>
     <swiper-slide>Slide 3</swiper-slide>
<!--     <swiper-slide>Slide 4</swiper-slide>-->
     <div class="swiper-pagination" slot="pagination"></div>
   </swiper>
 </div>
</template>

<script>
import { Swiper, SwiperSlide, directive } from 'vue-awesome-swiper'
import 'swiper/css/swiper.css'

export default {
  name: 'carrousel-view',
  components: {
    Swiper,
    SwiperSlide
  },
  directives: {
    swiper: directive
  },
  data() {
    return {
      swiperOptions: {
        loop: true,
        slidesPerView: 3,
        // threshold: 100, // 定义滑动的临界点为50像素
        spaceBetween: 30,
        centeredSlides: true,
        pagination: {
          el: '.swiper-pagination',
          clickable: true
        }
        // Some Swiper option/callback...
      }
    }
  },
  methods:{
    onTouchStart(event){
      this.startX = event.touches[0].clientX; // 获取触摸起始点的水平坐标
    },
    onTouchmove(event) {
      const threshold = 100
      const distance = event.touches[0].clientX - this.startX
      const isLeft = distance > 0
      const distanceAbs = Math.abs(distance) // 计算滑动距离
      console.log('滑动距离：' + distance + '像素');
      console.log(isLeft)

      if (distanceAbs > threshold) {
        this.swiper.allowTouchMove = false; // 禁止继续滑动s
      }
    },
    onTouchend(){
      this.swiper.allowTouchMove = true;
    },
  },
  computed: {
    swiper() {
      return this.$refs.mySwiper.$swiper
    }
  },
  mounted() {
    // console.log('Current Swiper instance object', this.swiper)
    // this.swiper.slideTo(3, 1000, false)
  }
}
</script>

<style lang="scss">
.swiper-container {
  height: 300px;
  width: 100%;

  .swiper-slide {
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    font-weight: bold;
    font-size: 16px;
    background-color: #2c3e50;
    color: #fff;
    transition: transform 0.4s ease; /* 添加滑动动画效果 */
    transform: scale(0.8); /* 默认缩小效果 */
  }

  /* 当前激活的幻灯片放大 */
  .swiper-slide.swiper-slide-active {
    transform: scale(1);
  }

  .swiper-slide.swiper-slide-duplicate-active {
    transform: scale(1);
  }
}
</style>

