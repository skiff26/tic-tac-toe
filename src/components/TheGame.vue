<template>
	<div class="game__container">
		<div class="board">
			<div class="board__row" v-for="(row, rowIndex) in board" :key="rowIndex">
				<div class="board__square" v-for="(square, colIndex) in row" :key="colIndex" :class="{'end-game' : end}" @click=" !end ? move(rowIndex, colIndex) : ''">
					<transition name="fade">
						<svg v-if="square" xmlns="http://www.w3.org/2000/svg" :width="wh" :height="wh" fill="#000000" class="bi bi-circle" viewBox="0 0 16 16" v-html="square"></svg>
					</transition>
				</div>
			</div>
		</div>
	</div>
</template>
<script>
import icons from '../icons';
export default {
	props: ['again'],
	watch: {
		again(){
			if (this.again){
			this.board = [
				['', '', ''],
				['', '', ''],
				['', '', ''],		
			]
			this.moveX = true
			this.end = false
			this.wh = 100
			this.$emit('update:again', !this.again);
			}
		}
	},
	data(){
		return {
			board: [
				['', '', ''],
				['', '', ''],
				['', '', ''],		
			],
			moveX: true,
			end: false,
			wh: 100,
		}
	},
	methods: {
		move(row, col){
			if (this.board[row][col] !== '') {
				alert('Данное поле занято')
				return
			} else {
				const icon = this.moveX ? icons['x'] : icons['circle']
				this.board[row][col] = icon
				this.moveX = !this.moveX
				this.$emit('move', this.moveX)
			}

			this.checkWinner(row, col, this.board)
			if (this.end === true){
				return
			} else {
				this.checkDraw()
			}
			
		},
		checkWinner(row, col, board){
			let count = 0

			for (let i = 0; i < 3; i++){
				if (board[i][col] === icons[!this.moveX ? 'x' : 'circle']){
					count++;
				}
			}
			
			this.ifWin(count)

			count = 0

			for (let i = 0; i < 3; i++){
				if (board[row][i] === icons[!this.moveX ? 'x' : 'circle']){
					count++;
				}
			}

			this.ifWin(count)

			count = 0

			for (let i = 0; i < 3; i++){
				if (board[i][i] === icons[!this.moveX ? 'x' : 'circle']){
					count++;	
				}
			}

			this.ifWin(count)

			count = 0

			for (let i = 0; i < 3; i++){
				if (board[i][2-i] === icons[!this.moveX ? 'x' : 'circle']){
					count++;	
				}
			}
			this.ifWin(count)
		},
		ifWin(count){
			if (count === 3) {
				this.end = true
				this.$emit("end", this.end)
				return true
			}
		},
		checkDraw(){
			let count = 0;

			for (let i = 0; i < this.board.length; i++) {
				for (let j = 0; j < this.board[i].length; j++) {
					if (this.board[i][j] !== ''){
						count++;
					}
				}
			}

			if(count === 9) {
				this.end = true
				this.$emit("draw", this.end)
				return
			}
		},
		onResize(){
			if (window.innerWidth < 380){
				this.wh = 70 
			} else {
				this.wh = 100
			}
		}
	},
	mounted() {
		this.onResize()
		window.addEventListener('resize', this.onResize)

	},
}
</script>