<script setup>
	import ChessMoveTracker from './components/ChessMoveTracker.vue'
</script>

<style scoped>
	.app-container {
		width: 100vw;
		height: 100vh;
		
		display: grid;
		grid-template-rows: min-content 1fr;
	}
	header {
		padding: 1em;
		text-align: center;
		transition: padding 0.2s; /* Smoothly transition if the window is resized across the media query threshold. */
	}
		header h1 {
			margin: 0;
			font-size: 1em;
			transition: font-size 0.2s;
		}

	@media (min-width: 600px) {
		header {
			padding: 1.5em;
		}
			header h1 {
				font-size: 1.5em;
			}
	}
</style>

<template>
	<div class="app-container">
		<header>
			<h1>Chess.com Frontend Test</h1>
		</header>
		<ChessMoveTracker />
	</div>
</template>
