<script>
	import Chessboard from './Chessboard.vue';
	import ChessMoveList from './ChessMoveList.vue';

	export default {
		components: {
			Chessboard,
			ChessMoveList
		},
		data() {
			return {
				/** {Array<String>} The list of selected squares in the order they were selected */
				squares: []
			}
		},
		methods: {
			/**
			 * Add a board square that was just selected to the list of selected squares.
			 * @param {String} squareName
			 */
			handleBoardSquareSelected(squareName) {
				this.squares.push(squareName);
			}
		}
	};
</script>

<style scoped>
	.chess-move-tracker {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		gap: calc(2 * var(--base-unit));
		min-height: 0; /* Prevent grid blowout. */
	}
	
	@media (orientation: landscape) {
		.chess-move-tracker {
			flex-direction: row;
		}
	}
	
	@media (min-width: 600px) {
		.chess-move-tracker {
			flex-direction: row;
			padding: calc(2 * var(--base-unit));
			padding-top: 0;
		}
	}
</style>

<template>
	<main class="chess-move-tracker">
		<Chessboard @selected="handleBoardSquareSelected" />
		<ChessMoveList :squares="squares" />
	</main>
</template>
