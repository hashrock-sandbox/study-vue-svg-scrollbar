<template>
  <div id="app">
    <svg width="300" height="200">
      <rect :x="item.x" :y="item.y" :width="item.w" :height="item.h"></rect>
      <rect :x="scrollx.x" y=190 :width="scrollx.w" height="10"></rect>
    </svg>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      item: {
        x: 100,
        y: 20,
        w: 100,
        h: 100
      },
      scrollx: {
        x: 0,
        w: 100
      }
    };
  }
};
</script>

<style>
svg {
  background: white;
}
body {
  background: gray;
}
</style>

