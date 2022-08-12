<script>
export default {
  // 组件选项
  data() {
    return {
      message: "Make me dynamic!",
      counter: {
        count: 10
      }
    };
  }
  // 此处声明一些响应式状态
};
</script>

<template>
  <h1>{{ message }}</h1>
  <p>{{ counter.count }}</p>
</template>
