<script setup lang="ts">
import { ref } from "vue";


const state = ref({
  show: true,
  notshow: false,
  playerX: "",
  playerO: "",
});

const emit = defineEmits(["addPlayers"]);


const handleSubmitPlayers = () => {
  emit("addPlayers", state.value.playerO, state.value.playerX);
  state.value.show = false;
  state.value.notshow = true;
};



</script>

<template>
  <div class="wrapper">
    <div v-if="state.show">
      <div>Spelare X - Spelare O</div>
      <form @submit.prevent="handleSubmitPlayers">
        <input type="text" v-model="state.playerX" />
        VS
        <input type="text" v-model="state.playerO" />
        <div><button>Spara</button></div>
      </form>
    </div>

    <div v-if="state.notshow" class="vs">
      <h3>{{ state.playerX }} <span>VS</span> {{ state.playerO }}</h3>
    </div>
  </div>
</template>

<style scoped>
.vs {
  padding-top: 50px;
}

.wrapper {
  display: flex;
  justify-content: center;

}

span {
  font-size: 12px;
}
</style>
