<template>
  <div ref="container" id="container">
    <div class="box">
      <Character/>
      <Pin v-for="pin in pinList" :text="pin.text" :position="pin.position"/>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
import { gsap } from "gsap";
import { Draggable } from "gsap/Draggable";
import Pin from '../components/Pin.vue'
import Character from '../components/Character.vue'

gsap.registerPlugin(Draggable);

export default {
  components: {
    Pin,
    Character
  },
  setup() {
    const container = ref(null)

    const pinList = [
      {
        text: "Festival",
        position: [360, 650],
      },
      {
        text: "Hotel",
        position: [770, 460],
      },
      {
        text: "Bateau",
        position: [528, 120],
      },
    ]

    onMounted(() => {
      function update() {
        Draggable.create(".box", {
          bounds:container.value,
          edgeResistance:0.65,
          type:"x,y",
          throwProps:true,
          autoScroll:true,
        });
      }

      update();
    })

    return {
      pinList,
      container,
    }
  }
}
</script>

<style scoped>
#container {
  background-color: #333;
  height:100%;
  width: 100%;
  overflow:hidden;
  position:relative;
}

.box {
  background-image: url("../assets/img/map2.jpg");
  background-size: 100%;
  background-position: center;
  width: 1200px;
  height: 1706px;
  position: absolute;
}
</style>