<template>
	<footer class="footer">
	<div class="footer__container">
		<ul class="footer__content">
			<h3 class="footer__item"><a href="https://en.wikipedia.org/wiki/Tic-tac-toe" target="_blank" class="footer__link">Крестики и нолики</a></h3>
			<li class="footer__item"><a href="https://en.wikipedia.org/wiki/Tic-tac-toe" target="_blank" class="footer__link">Правила игры</a></li>
			<li class="footer__item"><a href="mailto:artem.kulchitsky@gmail.com" class="footer__link">Сообщить об ошибке</a></li>
		</ul>
	</div>
	<div class="footer__copy">Copyright © {{ year }} All rights reserved</div>
	</footer>
</template>
<script>
export default {
	setup() {
		const year = new Date().getFullYear()
		return {
			year
		}
	}
}
</script>