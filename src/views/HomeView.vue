<template>
	<div class="wrapper">
		<TheHeader />
		<h1 class="page__title" v-once>Крестики и нолики</h1>
		  <main class="page">
			<button class="page__again" @click="tryAgain">
				<TryAgainButton />
			</button>
			<TheGame :again="again" @update:again="onAgainUpdate" @move="moveNow" @end="endGame" @draw="drawGame"/>	
			<transition name="fade">		
				<h2 class="page__move" v-show="!end && !draw">Ход {{ move }}</h2>
			</transition>
			<transition name="bounce">		
				<h2 class="page__win" v-show="end">Выиграл {{ move }}</h2>
			</transition>
			<transition name="bounce">		
				<h2 class="page__win" v-show="draw">Ничья</h2>
			</transition>
			</main>
		<TheFooter />
	</div>
</template>
<script>
import TheHeader from '../components/TheHeader.vue';
import TheFooter from '../components/TheFooter.vue';
import TheGame from '../components/TheGame.vue';
import TryAgainButton from '../components/TryAgainButton.vue';
export default {
	components: { TheHeader, TheFooter, TheGame, TryAgainButton },
	data(){
		return {
			moveX: true,
			end: false,
			draw: false,
			again: false,
		}
	},
	methods: {
		moveNow(moveX){
			this.moveX = moveX
		},
		endGame(end){
			this.end = end
		},
		drawGame(draw){
			this.draw = draw
		},
		tryAgain(){
			this.moveX = true
			this.end = false
			this.draw = false
			this.again = true
		},
		onAgainUpdate(newValue) {
			this.again = newValue
		}
	},
	computed: {
		move(){
			if (this.end){
				this.moveX = !this.moveX
			}
			return this.moveX ? "X" : "O"
		}
	},
	mounted(){
		const animatedElement = document.querySelector(".page__title");
   	animatedElement.classList.add("opacity");
	}
}
</script>