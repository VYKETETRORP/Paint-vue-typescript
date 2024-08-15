<template>
  <div class="toolbar">
    <button @click="increase">+</button>
    <span>{{ size }}</span>
    <button @click="decrease">-</button>
  </div>
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
    const size = ref (5)

    const DrawCircle = (x:number, y:number) => {
      let ctx = canvas.value?.getContext("2d");
      if (ctx) {
        ctx.beginPath();
        ctx.arc(x, y, size.value, 0, 2 * Math.PI);
        ctx.fill();
      }
    };
    const onMouseDown = (e:MouseEvent)=>{
      isMouseClicked = true
    

    }
    const onMouseMove = (e:MouseEvent)=>{
      if(isMouseClicked){
          let x = e.offsetX
      let y = e.offsetY
      DrawCircle(x,y);
      }
    }
    const onMouseUp = ()=>{
      isMouseClicked = false
    }
    onMounted(()=>{
      DrawCircle(200,200)
    })
    const increase = ()=>{
      size.value += 5
      if(size.value > 50){
        size.value=50
      }

    }
    const decrease = ()=>{
      size.value -= 5
      if(size.value < 5){
        size.value=5
      }

    }

    return {
      canvas,
      onMouseDown,
      onMouseMove,
      onMouseUp,
      increase,
      decrease,
      size,

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
</style>
