<template>
  <div class="pin">
    <span class="pin__marker"  :style="'top:' + position[0] + 'px; left:' + position[1] + 'px'" @click="clickPopUp($event)" @touchstart="clickPopUp"></span>
    <div class="pin__content" :style="'top:' + position[0] + 'px; left:' + (position[1] + 30) + 'px'" :class="{ active: isActive }">
      <p>{{ text }}</p>
    </div>
  </div>
</template>

<script>
import {ref} from "vue";
import ClickOutside from 'vue-click-outside'

export default {
  name: "Pin",
  props: ['text', 'position'],

  // do not forget this section
  directives: {
    ClickOutside
  },

  setup() {
    const isActive = ref(false)

    const clickPopUp = event => {
      if (!isActive.value) moveCharacter(event)
      isActive.value = !isActive.value
    }

    const moveCharacter = event => {
      const character = document.querySelector('.character')
      character.style.transform = `translateY(${event.srcElement.style.top}) translateX(calc(-100% + ${event.srcElement.style.left}))`
    }

    return {
      isActive,
      clickPopUp
    }
  }
}
</script>

<style scoped>

.pin__marker {
  width: 30px;
  height: 30px;
  background-color: red;
  border: 1px solid black;
  box-sizing: border-box;
  border-radius: 50px;
  position: absolute;
  cursor: pointer;
}

.pin__content {
  display: none;
  position: absolute;
  border: solid 1px black;
  background-color: white;
  padding: 20px 20px;
}

.pin__content.active {
  display: block;
}
</style>