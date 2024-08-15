<template>
  <canvas ref="canvas" height="500" width="500" @mousedown="onMouseDown"  @mousemove="onMouseMove" @mouseup="onMouseUp"></canvas>
</template>

<script lang="ts">
import { ref,onMounted } from "vue";
import { defineComponent } from "vue";
import HelloWorld from "./components/HelloWorld.vue";
export default defineComponent({
  name: "App",
  components: {
    HelloWorld,
  },
  setup() {
    const canvas = ref<HTMLCanvasElement>();
    let isMouseClicked = false

    const DrawCircle = (x:number, y:number) => {
      let ctx = canvas.value?.getContext("2d");
      if (ctx) {
        ctx.beginPath();
        ctx.arc(x, y, 20, 0, 2 * Math.PI);
        ctx.fill();
      }
    };
    const onMouseDown = (e:MouseEvent)=>{
      isMouseClicked = true
      let x = e.offsetX
      let y = e.offsetY
      DrawCircle(x,y);

    }
    const onMouseMove = (e:MouseEvent)=>{
      let x = e.offsetX
      let y = e.offsetY
      DrawCircle(x,y);

    }
    const onMouseUp = ()=>{

    }

    
    onMounted(()=>{
      DrawCircle(200,200)
    })

    return {
      canvas,
      onMouseDown,
      onMouseMove,
      onMouseUp,
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
}
canvas {
  border: 1px solid black;
}
</style>
