<script>
	export default {
		props: {
			squares: {
				type: Array,
				default: []
			}
		}
	};
</script>

<style scoped>
	.chess-move-list {
		width: 100%;
		flex-grow: 1;
		flex-shrink: 1;
		padding: calc(2 * var(--base-unit)) 0;
		overflow-y: auto;
		
		background-color: var(--color-surface);
	}
		.chess-move-list p {
			text-align: center;
			font-style: italic;
		}
		.chess-move-list ol {
			margin: 0;
			padding: 0;
			list-style-type: none;
		}
		.chess-move-list li {
			padding: calc(2 * var(--base-unit)) calc(6 * var(--base-unit));
		}
	
	@media (orientation: landscape) {
		.chess-move-list {
			height: 100%;
			border-top-left-radius: calc(2 * var(--base-unit));
		}
	}
	
	@media (min-width: 600px) {
		.chess-move-list {
			width: auto;
			max-width: 16em;
			height: 100%;
			border-radius: calc(2 * var(--base-unit));
		}
	}
</style>

<template>
	<div class="chess-move-list">
		<ol v-if="squares?.length > 0">
			<li v-for="square in squares.slice().reverse()">{{ square }}</li>
		</ol>
		<p v-else style="font-style: italic;">Select a<br />board square</p>
	</div>
</template>
