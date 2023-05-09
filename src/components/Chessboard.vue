<script>
	export default {
		data() {
			return {
				/** {String} The name of the currently selected square, if any */
				selectedSquare: undefined
			};
		},
		methods: {
			/**
			 * Get the name of a given square in the linear list of chessboard squares.
			 * @param {Number} col
			 * @param {Number} row
			 * @returns {String}
			 */
			getSquareName(col, row) {
				return ('ABCDEFGH'.charAt(col)) + (8 - row);
			},
			
			/**
			 * Check whether the given square is currently selected.
			 * @param {Number} col
			 * @param {Number} row
			 * @returns {Boolean}
			 */
			isSelected(col, row) {
				return this.getSquareName(col, row) === this.selectedSquare;
			},
			
			/**
			 * Handle a board square being clicked.
			 * @param {MouseEvent|PointerEvent} ev
			 */
			handleClick(ev) {
				this.selectedSquare = ev.currentTarget.dataset.name;
				this.$emit('selected', ev.currentTarget.dataset.name);
			}
		}
	};
</script>

<style scoped>
	.chessboard {
		flex-shrink: 0; /* Maintain square board; resize list panel around it. */
		width: 100%;
		max-width: calc(100vh - 6em); /* This will also be the max-height because it is square. */
		aspect-ratio: 1 / 1;
		
		display: grid;
		grid-template-rows: repeat(8, auto);
		/*grid-template-columns: repeat(8, auto);*/ /* Chrome still hasn't shipped subgrid. */
		gap: calc(0.5 * var(--base-unit)); /* Leave less space between squares in small windows. */
		
		background-color: var(--color-board-bg);
		border-radius: calc(2 * var(--base-unit));
		padding: calc(2 * var(--base-unit));
	}
	
	.chessboard-row {
		display: grid;
		grid-column: 1 / 9;
		grid-template-rows: 1fr;
		/*grid-template-columns: subgrid;*/ /* Chrome still hasn't shipped subgrid. */
		grid-template-columns: repeat(8, auto);
		gap: calc(0.5 * var(--base-unit));
	}
	
	.chessboard-square {
		border: 0 none;
		border-radius: var(--base-unit);
		background-color: var(--color-board-white);
		cursor: pointer;
		
		position: relative;
		overflow: hidden;
		
		transition: transform 0.1s;
	}
		.chessboard-row:nth-child(even) .chessboard-square:nth-child(odd),
		.chessboard-row:nth-child(odd) .chessboard-square:nth-child(even) {
			background-color: var(--color-board-black);
		}
		.chessboard-square:hover,
		.chessboard-square:focus-visible {
			transform: scale(1.05);
			z-index: 1;
		}
		.chessboard-square:active {
			transform: scale(0.95);
		}
		
		.chessboard-square.selected::after {
			/* Translucent accent color overlay on the selected square. */
			content: '';
			display: block;
			position: absolute;
			left: 0;
			right: 0;
			top: 0;
			bottom: 0;
			background-color: var(--color-accent-30);
			box-shadow: inset 0 0 var(--base-unit) var(--base-unit) var(--color-accent);
		}
			.chessboard-row:nth-child(even) .chessboard-square:nth-child(odd).selected::after,
			.chessboard-row:nth-child(odd) .chessboard-square:nth-child(even).selected::after {
				/* Weaker glow on dark squares. */
				/* Copy/pasted selector because Firefox hasn't shipped nesting yet, but obviously could also use a preprocessor. */
				box-shadow: inset 0 0 calc(2 * var(--base-unit)) calc(0.5 * var(--base-unit)) var(--color-accent-30);
			}
	
	@media (min-width: 600px) {
		.chessboard {
			width: auto;
			flex-grow: 2;
			gap: var(--base-unit);
		}
		.chessboard-row {
			gap: var(--base-unit);
		}
	}
</style>

<template>
	<div class="chessboard" role="grid">
		<div v-for="row in 8" class="chessboard-row" role="row">
			<button
				v-for="col in 8"
				type="button"
				role="gridcell"
				class="chessboard-square"
				:data-name="getSquareName(col - 1, row - 1)"
				:aria-label="getSquareName(col - 1, row - 1)"
				:class="isSelected(col - 1, row - 1) ? 'selected' : ''"
				:aria-selected="isSelected(col - 1, row - 1) ? 'true' : 'false'"
				@click="handleClick" />
		</div>
	</div>
</template>
