<template>
    <div class="tic-tac-toe-widget">
      <h2 class="widget-title">Tic Tac Toe</h2>
      <div class="board">
        <div
          v-for="(cell, index) in board"
          :key="index"
          @click="handleClick(index)"
          class="cell"
          :class="{ 'cell-x': cell === 'X', 'cell-o': cell === 'O' }"
        >
          {{ cell }}
        </div>
      </div>
      <button class="reset-button" @click="resetGame">Mulai Ulang</button>
      <p class="status">{{ status }}</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        board: ['', '', '', '', '', '', '', '', ''],
        currentPlayer: 'X',
        isGameEnded: false,
        isAgainstBot: true,
        resultMessage: '',
      };
    },
    computed: {
      status() {
        if (this.isGameEnded) {
          return this.resultMessage;
        }
        return this.isAgainstBot
          ? `Player ${this.currentPlayer}'s turn`
          : "Player's turn";
      },
    },
    methods: {
      handleClick(index) {
        if (!this.isGameEnded && this.board[index] === '') {
          this.board[index] = this.currentPlayer;
          this.checkWinner();
  
          if (!this.isGameEnded) {
            if (this.isAgainstBot) {
              this.makeBotMove();
            } else {
              this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
            }
          }
        }
      },
      checkWinner() {
        const winningCombinations = [
          [0, 1, 2],
          [3, 4, 5],
          [6, 7, 8], // Rows
          [0, 3, 6],
          [1, 4, 7],
          [2, 5, 8], // Columns
          [0, 4, 8],
          [2, 4, 6], // Diagonals
        ];
  
        for (const combination of winningCombinations) {
          const [a, b, c] = combination;
          if (
            this.board[a] &&
            this.board[a] === this.board[b] &&
            this.board[a] === this.board[c]
          ) {
            this.isGameEnded = true;
            this.resultMessage =
              this.currentPlayer === 'X' ? 'kamu menang wow!' : 'kamu kalah !';
            return;
          }
        }
  
        if (!this.board.includes('')) {
          this.isGameEnded = true;
          this.resultMessage = "wah seri!";
        }
      },
      makeBotMove() {
        const availableMoves = this.board.reduce((moves, cell, index) => {
          if (cell === '') {
            moves.push(index);
          }
          return moves;
        }, []);
  
        const randomIndex = Math.floor(Math.random() * availableMoves.length);
        const botMove = availableMoves[randomIndex];
  
        this.board[botMove] = 'O';
        this.checkWinner();
        this.currentPlayer = 'X';
      },
      resetGame() {
        this.board = ['', '', '', '', '', '', '', '', ''];
        this.currentPlayer = 'X';
        this.isGameEnded = false;
        this.resultMessage = '';
      },
    },
  };
  </script>
  
  <style scoped>
  .tic-tac-toe-widget {
    border: 1px solid #ccc;
    padding: 20px;
    margin-bottom: 20px;
    text-align: center;
    background-color: #0fc7ff;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }
  
  .widget-title {
    margin-top: 0;
    color: #333;
  }
  
  .board {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 10px;
    margin-bottom: 10px;
  }
  
  .cell {
    border: 1px solid #ccc;
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    font-size: 40px;
    font-weight: bold;
    transition: background-color 0.3s;
    background-color: #fff;
    border-radius: 5px;
  }
  
  .cell:hover {
    background-color: #eee;
  }
  
  .cell-x {
    color: #ff1f5a;
  }
  
  .cell-o {
    color: #1992ff;
  }
  
  .reset-button {
    margin-top: 10px;
    background-color: #47b7ed;
    color: #fff;
    border: none;
    padding: 10px 20px;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .reset-button:hover {
    background-color: #2f97c3;
  }
  
  .status {
    font-weight: bold;
    font-size: 20px;
    color: #333;
  }
  </style>
  