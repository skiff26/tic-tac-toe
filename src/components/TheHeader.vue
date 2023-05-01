<template>
	<header class="header">
		<div class="header__container">
			<ul class="header__content">
				<li class="header__item"
				v-for="item in links" :key="item.link">
					<a :href="item.link" target="_blank" class="header__link">{{ item.label }}</a>
				</li>
			</ul>
		</div>
	</header>
</template>
<script setup>
	const links = [
		{
			link: 'https://skiff26.github.io/portfolio/#/',
			label: 'Автор'
		},
		{
			link: 'https://skiff26.github.io/chess/',
			label: 'Шахматы'
		},
		{
			link: 'mailto:artem.kulchitsky@gmail.com',
			label: 'Почта'
		},
	]
</script>