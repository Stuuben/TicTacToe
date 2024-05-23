<script setup lang="ts">
import { Player } from '../models/Player';


interface IHighScoreProp {
  players: Player[]

}

const prop = defineProps<IHighScoreProp>()


</script>

<template>
  <div class="wrapper">
    <table>
      <th> Namn </th>
      <th> Poäng </th>
      <tr v-for="player in players">
        <td> {{ player.name }}</td>
        <td>{{ player.score }}</td>
      </tr>

    </table>
  </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
  margin: 0;
}

th {
  padding: 10px;
}
</style>