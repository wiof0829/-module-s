<template>
  <div id="date_time_picker">
    <!-- 开始时间 输入框 -->
    <van-field
      v-model="startValue"
      placeholder="开始时间"
      readonly
      label="开始时间"
      @click="showStartTime()"
    />
    <!-- 结束时间 输入框 -->
    <van-field
      v-model="endValue"
      placeholder="结束时间"
      readonly
      label="结束时间"
      @click="showEndTime()"
    />
    <!-- 开始 弹出层 -->
    <van-popup v-model="showStart" position="bottom" :style="{ height: '40%' }">
      <van-datetime-picker
        v-model="startTime"
        type="datetime"
        :max-date="currentTime"
        @confirm="confirmStartFn()"
        @cancel="cancelFn()"
      />
    </van-popup>
    <!-- 结束 弹出层 -->
    <van-popup v-model="showEnd" position="bottom" :style="{ height: '40%' }">
      <van-datetime-picker
        v-model="endTime"
        type="datetime"
        :min-date="currentTime"
        @confirm="confirmEndFn()"
        @cancel="cancelFn()"
      />
    </van-popup>
  </div>
</template>
 
<script>
export default {
  data() {
    return {
      startValue: "", //输入框默认值
      endValue: "",
      currentTime: new Date(), // 开始时间不能超过当前时间
      startTime: new Date(), // 开始时间
      endTime: new Date(), // 开始时间
      showStart: false, // 用来显示弹出层
      showEnd: false,
    };
  },
  methods: {
    showStartTime() {
      this.showStart = true;
    },
    showEndTime() {
      this.showEnd = true;
    },
    confirmStartFn() {
      // 确定按钮
      this.startValue = this.timeFormat(this.startTime);
      this.showStart = false;
    },
    confirmEndFn() {
      this.endValue = this.timeFormat(this.endTime);
      this.showEnd = false;
      console.log(this.startValue,this.endTime)
    },
    cancelFn() {
      this.showStart = false;
    },
    timeFormat(time) {
      // 时间格式化 2019-09-08
      let year = time.getFullYear();
      let month = time.getMonth() + 1;
      let day = time.getDate();
       let hour = time.getHours();
      let minute = time.getMinutes();
      return year + "年" + month + "月" + day + "日" + hour + '|' + minute;
    },
  },
  mounted() {
    this.timeFormat(new Date());
  },
};
</script>
<style scoped>
input {
  color: red;
}
</style>

