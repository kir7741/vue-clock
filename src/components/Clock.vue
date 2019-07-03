<template>
  <div class="wrapper">
    <div class="clock-box">
      <div 
        class="spinner hour"
        :style="{ transform: 'rotate(' + hourDeg + 'deg)' }"
      ></div>
      <div 
        class="spinner minute"
        :style="{ transform: 'rotate(' + minuteDeg + 'deg)' }"
      ></div>
      <div 
        class="spinner second"
        :style="{ transform: 'rotate(' + secondDeg + 'deg)' }"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Clock',
  data() {
    return {
      timer: null,
      hourDeg: 0,
      minuteDeg: 0,
      secondDeg: 0
    }
  },
  mounted() {
    this.calcTime();
  },
  destroyed() {
    clearInterval(this.timer);
  },
  methods: {
    calcTime() {

      this.timer = setInterval(() => {

        // 取得時、分、秒的時間
        const date = new Date();
        const nowHr = date.getHours();
        const nowMin = date.getMinutes();
        const nowSec = date.getSeconds();

        // 計算時針角度時，需額外計算分針所帶來的角度偏移
        const hourDeg = 360 / 12 * nowHr;

        // 時針，每小時間隔 30度
        const hourScale = 360 / 12;

        // 取得額外的時針角度
        const extraHourDeg = Math.ceil(hourScale * (nowMin / 60));

        this.hourDeg = hourDeg + extraHourDeg;
        this.minuteDeg = 360 / 60 * nowMin;
        this.secondDeg = 360 / 60 * nowSec - 180;

      }, 1000);

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@mixin hand($bgUrl) {
  content: '';
  position: absolute;
  margin: 0 auto;
  background-image: url($bgUrl);
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
}
 
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.clock-box {
  position: relative;
  width: 350px;
  height: 350px;
  background-image: url('../assets/images/clock-bg.svg');
  background-repeat: no-repeat;
  background-position: center center;
}
.spinner {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  &.hour {
    margin: 0 auto;
    width: 8px;
    &:before {
      @include hand('../assets/images/hour-hand.svg');
      width: 8px;
      height: 72px;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -99%);
    }
  }
  &.minute {
    margin: 0 auto;
    width: 8px;
    &:before {
      @include hand('../assets/images/minute-hand.svg');
      width: 8px;
      height: 96px;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -99%);
    }
  }
  &.second {
    margin: 0 auto;
    width: 8px;
    &:before {
      @include hand('../assets/images/second-hand.svg');
      width: 8px;
      height: 120px;
      left: 50%;
      bottom: 0;
      transform: translate(-50%, -46%);
    }
  }
}
@media screen and (min-width: 992px) {
  .wrapper {
    min-height: 800px;
  }
}
</style>
