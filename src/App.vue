<template>
  <div class="toolbar">
    <button @click="increase">+</button>
    <span>{{ size }}</span>
    <button @click="decrease">-</button>
    <input type="color" @change="handleColorChange" />
    <button @click="clearCanvas">&#9746;</button>
  </div>
  <canvas
    ref="canvas"
    height="500"
    width="500"
    @mousedown="onMouseDown"
    @mousemove="onMouseMove"
    @mouseup="onMouseUp"
  ></canvas>
</template>

<script lang="ts">
import { ref, onMounted } from "vue";
import { defineComponent } from "vue";
import HelloWorld from "./components/HelloWorld.vue";
export default defineComponent({
  name: "App",
  components: {
    HelloWorld,
  },
  setup() {
    const canvas = ref<HTMLCanvasElement>();
    let isMouseClicked = false;
    const size = ref(5);
    let color = "#111";

    const DrawCircle = (x: number, y: number) => {
      let ctx = canvas.value?.getContext("2d");
      if (ctx) {
        ctx.beginPath();
        ctx.arc(x, y, size.value, 0, 2 * Math.PI);
        ctx.fillStyle = color;
        ctx.fill();
      }
    };
    const onMouseDown = (e: MouseEvent) => {
      isMouseClicked = true;
    };
    const onMouseMove = (e: MouseEvent) => {
      if (isMouseClicked) {
        let x = e.offsetX;
        let y = e.offsetY;
        DrawCircle(x, y);
      }
    };
    const onMouseUp = () => {
      isMouseClicked = false;
    };
    onMounted(() => {
      DrawCircle(200, 200);
    });
    const increase = () => {
      size.value += 5;
      if (size.value > 50) {
        size.value = 50;
      }
    };
    const decrease = () => {
      size.value -= 5;
      if (size.value < 5) {
        size.value = 5;
      }
    };
    const handleColorChange = (e: Event) => {
      let eventTarget = e.target as HTMLInputElement;
      color = eventTarget.value;
    };
    const clearCanvas = () => {
      let ctx = canvas.value?.getContext("2d");
      if (ctx && canvas.value) {
        ctx.fillStyle = "rgb(255,255,255)";
        ctx.fillRect(0, 0, canvas.value.width, canvas.value.height);
      }
    };

    const drawLine = (x1:number , y1:number , x2:number , y2:number) => {
      let ctx = canvas.value?.getContext("2d");
      if (ctx) {
        ctx.beginPath();
        ctx.moveTo(x1, y1);
        ctx.lineTo(x2, y2);
        ctx.stroke();
      }
    };

    return {
      canvas,
      onMouseDown,
      onMouseMove,
      onMouseUp,
      increase,
      decrease,
      size,
      handleColorChange,
      color,
      clearCanvas,
      drawLine,
    };
  },
});
</script>

<style>
body {
  margin: 0;
  display: flex;
  justify-content: center;
  min-height: 100vh;
  align-items: center;
  flex-direction: column;
}
canvas {
  border: 1px solid black;
}
.toolbar {
  width: 483px;
  background-color: rgb(68, 68, 148);
  padding: 10px;
  display: flex;
}
.toolbar * {
  margin-right: 10px;
  height: 30px;
  width: 30px;
  background-color: #fff;
}
.toolbar span {
  display: inline-flex;
  align-items: center;
  justify-content: center;
}
.toolbar *:last-child {
  margin-left: auto;
}
</style>
