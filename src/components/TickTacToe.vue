<script setup lang="ts">
import { Player } from "../models/Player";
import AddPlayers from "./AddPlayers.vue";
import PlayGame from "./PlayGame.vue";
import { Square } from "../models/Square";
import { ref } from "vue";
import HighScore from "./HighScore.vue";

// Players

const players = ref<Player[]>([]);

const handlePlayers = (playerO: string, playerX: string) => {
  players.value.push(new Player(playerX, 0, "X"));
  players.value.push(new Player(playerO, 0, "O"));
};

//
ref
//Game

interface IGamePlayers {
  name: string;
  win: boolean;
  clickedSquare: ICheckSquare[];

}

interface IGame {
  squares: Square[];
  currentPlayer: number;
  showDraw: boolean
  showWinner: boolean
}
interface ICheckSquare {
  id: number;
}

const game = ref<IGame>({
  showDraw: false,
  showWinner: false,

  squares: [
    { id: 0, clicked: false, symbol: "" },
    { id: 1, clicked: false, symbol: "" },
    { id: 2, clicked: false, symbol: "" },
    { id: 3, clicked: false, symbol: "" },
    { id: 4, clicked: false, symbol: "" },
    { id: 5, clicked: false, symbol: "" },
    { id: 6, clicked: false, symbol: "" },
    { id: 7, clicked: false, symbol: "" },
    { id: 8, clicked: false, symbol: "" },
  ],
  currentPlayer: 0,

});

game.value.currentPlayer


const possibleWins = [
  [0, 1, 2],
  [3, 4, 5],
  [6, 7, 8],
  [0, 3, 6],
  [1, 4, 7],
  [2, 5, 8],
  [0, 4, 8],
  [2, 4, 6],
];

const checkIfWin = () => {
  for (const rowToCheck of possibleWins) {
    const index0 = rowToCheck[0];
    const square0 = game.value.squares[index0];
    const index1 = rowToCheck[1];
    const square1 = game.value.squares[index1];
    const index2 = rowToCheck[2];
    const square2 = game.value.squares[index2];


    if (
      square0.symbol !== "" &&
      square0.symbol === square1.symbol &&
      square1.symbol === square2.symbol
    ) {
      console.log("all same symbols", square0.symbol);

      return square0.symbol;
    }
  }
  return "";
};



function checkIfClicked() {
  for (let i = 0; i < game.value.squares.length; i++) {
    if (!game.value.squares[i].clicked) {
      return false;
    }
  }
  return true;
}

const currentClickedSquare = (index: number) => {
  game.value.currentPlayer = game.value.currentPlayer === 0 ? 1 : 0;

  if (game.value.squares[index].symbol === "") {
    game.value.squares[index].symbol =
      game.value.currentPlayer === 0 ? "X" : "O";
  }


  const winnerSymbol = checkIfWin();
  if (winnerSymbol !== "") {
    game.value.showWinner = true
    console.log("Winner is:", winnerSymbol);
    for (let i = 0; i < game.value.squares.length; i++) {
      game.value.squares[i].clicked = true;
    }

  }
  if (winnerSymbol === "O") {
    players.value[0].score++;
    console.log("playerO point:", players.value[0]);
  }
  if (winnerSymbol === "X") {
    players.value[1].score++;
    console.log("playerX point:", players.value[1]);
  }
  if (!game.value.squares[index].clicked) {
    game.value.squares[index].clicked = true;
    console.log("square cliked", game.value.squares[index].clicked);
  }
  if (checkIfClicked()) {
    console.log("DRAW");

  }
  if (checkIfClicked() && !game.value.showWinner) {
    game.value.showDraw = true
  }


  console.log("Toggle player", game.value.currentPlayer);
  console.log(game.value.squares);

  console.log(game.value.squares[index]);
};
const playAgain = () => {

  for (let i = 0; i < game.value.squares.length; i++) {
    game.value.squares[i].symbol = "";
    game.value.squares[i].clicked = false

  }
  game.value.showDraw = false
  game.value.showWinner = false

  console.log(game.value.squares);
};



//


//
</script>

<template class="wrapper">
  <h1>Tic Tac Toe</h1>

  <AddPlayers @add-players="handlePlayers"></AddPlayers>
  <div>Det är spelare {{ game.currentPlayer }} tur</div>
  <div class="container">
    <PlayGame :squares="square" v-for="(square, index) in game.squares" :class="square.symbol"
      @current-clicked-square="currentClickedSquare(index)">
    </PlayGame>
  </div>
  <div v-if="game.showDraw">DRAW!</div>
  <div v-if="game.showWinner">WINNER</div>
  <button @click="playAgain">Spela Igen</button>
  <form @submit=""><button @click="">Starta Om Från Början</button></form>
  <!-- ful lösning -->

  <HighScore :players="players"></HighScore>
</template>

<style scoped>
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 5px;
  width: 400px;
  height: 400px;
}



.X {
  background-color: red;
}

.O {
  background-color: rgb(53, 184, 53);
}
</style>
