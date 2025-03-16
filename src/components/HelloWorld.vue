<template>
  <div>
    <h1>Tic Tac Toe</h1>
    <hr>
    <h1>現在是誰:{{ getSymbol(player)}} winner :{{ getSymbol(winner) }}</h1>
    <button @click="reset">重製</button>
    <div class="grids">
      <div class="gird" v-for="(grid, index) in grid" :key="index" @click="clickGrid(index)">
        {{ getSymbol(grid) }}
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: 'HelloWorld',

  data() {
    return {
      grid: [0, 0, 0
        , 0, 0, 0
        , 0, 0, 0],
      player: 1,
      winner: 0,
    }
  },
  methods: {
    clickGrid(index: number) {
      if (this.grid[index] !== 0)
        return;
      if (this.winner !== 0){
        return;
      }
      // this.$set(this.grid,index,this.player);
      this.grid[index] = this.player; //原本是 0 改成1 或 -1
      this.player = -this.player; //換人
      this.checkWinner(); //這邊要加他才會 每次都判斷
    },
    getSymbol(index: number) {
      if (index === 1) return 'O';
      if (index === -1) return 'X';
      return '';
      // 也可以這樣寫 
      // return index === 0 ? '' : index === 1 ? 'O' : 'X';
    },
    checkWinner() {

      const winPatterns = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8], // Rows
        [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columns
        [0, 4, 8], [2, 4, 6]             // Diagonals
      ]
      for (let pattern of winPatterns){
        const [a,b,c] = pattern;
        if (this.grid[a] !== 0 && this.grid[a] === this.grid[b] && this.grid[a] === this.grid[c]){
          this.winner = this.grid[a];
        }
        
      }
    },
    reset(){
      this.grid=[0,0,0,0,0,0,0,0,0];
      this.player=1;
      this.winner=0;
    }
  }
}
</script>

<style scoped>
h1 {
  text-align: center;
}

.grids {
  display: grid;
  border: 1px solid #333;
  grid-template-columns: repeat(3, 1fr);
  /* 3 columns */
  grid-gap: 5px;
  width: 500px;
  margin: 0 auto;
}

.gird {
  background: #f4f4f4;
  padding: 30px;
  border-radius: 5px;
  text-align: center;
  cursor: pointer;
}
</style>