<script setup lang="ts">
import { ref } from "vue";
import { Square } from "../models/Square";

interface IPlayGameProp {
  squares: Square;
}
interface INoClick {
  noClick: boolean;
}

const state = ref<INoClick>({
  noClick: false,
});

const props = defineProps<IPlayGameProp>();

const emit = defineEmits(["currentClickedSquare"]);

const handleSquare = () => {
  emit("currentClickedSquare");
  state.value.noClick = true;
};
</script>

<template>
  <div @click="handleSquare" class="square" :class="squares.clicked ? 'noClick' : null">
    <!-- {{ props.squares.id }} -->
  </div>
</template>

<style scoped>
.square {

  background-color: rgb(217, 224, 224);
  border: 1px black solid;
  border-radius: 10px;

}

.noClick {
  pointer-events: none;

}
</style>
