<script setup lang="ts">
	// This starter template is using Vue 3 <script setup> SFCs
	// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup

	import Main from "./components/MainContainer.vue";
</script>

<template>
	<h1>Spli<br />tter</h1>
	<Main />
</template>

<style>
	:root {
		--c-cyan: hsl(172, 67%, 45%);

		/* Neutral */
		--c-very-dark-cyan: hsl(183, 100%, 15%);
		--c-Dark-grayish-cyan: hsl(186, 14%, 43%);
		--c-Dark-grayish-cyan-2: hsl(184, 14%, 56%);
		--c-Light-grayish-cyan: hsl(185, 41%, 84%);
		--c-Light-grayish-cyan-2: hsl(189, 41%, 97%);
		--c-White: hsl(0, 0%, 100%);
	}
	body {
		font-family: "Space Mono", monospace;
		font-size: 24px;
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: var(--c-Light-grayish-cyan);
	}
	h1 {
		color: var(--c-very-dark-cyan);
		text-align: center;
	}
	@media screen and (max-width: 900px) {
		#app {
			width: 100vw;
		}
	}
</style>
