<template>
  <img src="../assets/img/character.png" alt="Charater" class="character">
</template>

<script>
export default {
name: "Character"
}
</script>

<style scoped>
.character {
  height: 80px;
  position: absolute;
  top: 0;
  left: 0;
  transition: transform 2s;
}
</style>