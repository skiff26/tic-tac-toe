<template>
	<footer class="footer">
	<div class="footer__container">
		<ul class="footer__content">
			<li class="footer__item" v-for="item in links" :key="item.label">
				<a :href="item.link" :target="item.self ? '_self' : '_blank'" class="footer__link">{{ item.label }}</a>
			</li>
		</ul>
	</div>
	<div class="footer__copy">Copyright © {{ year }} All rights reserved</div>
	</footer>
</template>
<script setup>
	const year = new Date().getFullYear()
	const links = [
		{
			link: 'https://en.wikipedia.org/wiki/Tic-tac-toe',
			label: 'Крестики и нолики',
		},
		{
			link: 'https://en.wikipedia.org/wiki/Tic-tac-toe',
			label: 'Правила игры',
		},
		{
			link: 'mailto:artem.kulchitsky@gmail.com',
			label: 'Сообщить об ошибке',
			self: true,
		},
	]
</script>