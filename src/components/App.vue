<template>
  <div id="app">
    <svg width="300" height="200" @pointermove="onpointermove" @pointerup="onpointerup">
      <rect :x="item.x" :y="item.y" :width="item.w" :height="item.h"></rect>
      <rect :x="scrollx.x" y=190 :width="scrollx.w" height="10"  @pointerdown="onpointerdown"></rect>
    </svg>
  </div>
</template>

<script>
let scrollBarEl;

export default {
  name: "app",
  methods: {
    onpointermove(e) {
      if (this.dragging) {
        const bound = e.currentTarget.getBoundingClientRect();
        const x = e.clientX - bound.left;
        this.offset = (x - this.dragOffset) / this.svg.w * this.area.w;
      }
    },
    onpointerup(e) {
      this.dragging = false;
      scrollBarEl.releasePointerCapture(e.pointerId);
    },
    onpointerdown(e) {
      const bound = e.currentTarget.getBoundingClientRect();
      this.dragOffset = e.clientX - bound.left;
      this.dragging = true;
      scrollBarEl = e.target;
      e.target.setPointerCapture(e.pointerId);
    },
    onmousemove(e) {
      console.log(e.offsetX);
      this.offset = e.offsetX / this.svg.w * this.area.w;
    }
  },
  computed: {
    item() {
      return {
        x: (this.src.x - this.offset) * this.scale,
        y: this.src.y,
        w: this.src.w * this.scale,
        h: this.src.h
      };
    },
    viewport() {
      return {
        x: this.offset,
        y: 0,
        w: this.svg.w / this.scale,
        h: this.svg.h
      };
    },
    scrollx() {
      return {
        x: this.offset / this.area.w * this.svg.w,
        w: this.viewport.w / this.area.w * this.svg.w
      };
    }
  },
  data() {
    return {
      dragOffset: 0,
      dragging: false,
      svg: {
        w: 300,
        h: 200
      },
      scale: 1,
      offset: 0,
      src: {
        x: 100,
        y: 20,
        w: 100,
        h: 100
      },
      area: {
        w: 1200,
        h: 200
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

