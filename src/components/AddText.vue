<template>
  <div class="sticky" style="margin-left: 45%; width: 130px">
    <p v-for="(item, index) in poem" :key="index" :style="getStyle(item)">
      {{ item.text }}
    </p>
  </div>
</template>
<script setup>
import { ref, watchEffect } from "vue";
const props = defineProps({
  arr: {
    default: [],
  },
  // 字体颜色(R,G,B)
  color: {
    default: "255, 192, 203",
  },
  // 字体大小
  fontsize: {
    default: "14px",
  },
});

const INTERVAL = 50; //每一行显示间隔
const SPEED = 0.1; //显示速度
const poem = ref([]);

const getStyle = (item) => {
  let percentage = 0;
  if (item.percentage > 0) {
    percentage = item.percentage;
  }
  if (item.percentage > 100) {
    percentage = 100;
  }
  return {
    "--percentage": `${percentage}%`,
    fontSize: props.fontsize,
    backgroundImage: `linear-gradient(75deg, rgba(${props.color}, 1) 0%, rgba(${props.color}, 1) 33.33%, rgba(${props.color}, 0) 66.67%, rgba(${props.color}, 0) 100%)`,
  };
};

const enterFrame = () => {
  poem.value.forEach((item) => {
    item.percentage += SPEED;
  });
  requestAnimationFrame(enterFrame);
};
enterFrame();

watchEffect(() => {
  poem.value = props.arr.map((text, index) => ({ text, percentage: index * -INTERVAL }));
});
</script>
<style scoped lang="scss">
.sticky {
  position: sticky;
  top: 0;
  justify-content: center;
  align-items: center;
}

p {
  --percentage: 0%;
  display: inline-block; /* 或者 display: inline; */
  margin: 0 5px;
  font-family: ysbth;
  font-size: 10px;
  width: 150px;

  letter-spacing: -0.3px;
  background-size: 300% 100%;
  background-position-x: calc(100% - var(--percentage));
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
}
</style>
