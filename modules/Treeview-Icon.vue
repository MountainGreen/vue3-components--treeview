<template>

<!-- Plus squared -->
<svg
	v-if="type === 'plus-square'"
	:width="`${TOGGLE_SIZE / 2}`"
	:height="`${TOGGLE_SIZE / 2}`"
	viewBox="0, 0, 25, 25"
	xmlns="http://www.w3.org/2000/svg"
>
	<path fill="#000000" d="m11.97645,4.82575c0.66025,0 1.19545,0.53593 1.19545,1.19702l0,4.78806l4.78179,0c0.66025,0 1.19545,0.5359 1.19545,1.19702c0,0.66111 -0.5352,1.19702 -1.19545,1.19702l-4.78179,0l0,4.78806c0,0.66111 -0.5352,1.19702 -1.19545,1.19702c-0.66025,0 -1.19545,-0.5359 -1.19545,-1.19702l0,-4.78806l-4.78179,0c-0.66022,0 -1.19545,-0.5359 -1.19545,-1.19702c0,-0.66111 0.53523,-1.19702 1.19545,-1.19702l4.78179,0l0,-4.78806c0,-0.66109 0.5352,-1.19702 1.19545,-1.19702z"/>
	<path fill="#000000" d="m0.02199,3.03023c0,-1.65273 1.33805,-2.99254 2.98862,-2.99254l17.9317,0c1.65055,0 2.98862,1.33981 2.98862,2.99254l0,17.95524c0,1.65272 -1.33806,2.99254 -2.98862,2.99254l-17.9317,0c-1.65056,0 -2.98862,-1.33982 -2.98862,-2.99254l0,-17.95524zm2.98862,-0.59851c-0.33011,0 -0.59772,0.26796 -0.59772,0.59851l0,17.95524c0,0.3305 0.26761,0.59851 0.59772,0.59851l17.9317,0c0.33006,0 0.59772,-0.26801 0.59772,-0.59851l0,-17.95524c0,-0.33054 -0.26766,-0.59851 -0.59772,-0.59851l-17.9317,0z" clip-rule="evenodd" fill-rule="evenodd"/>
</svg>

<!-- Minus squared -->
<svg
	v-if="type === 'minus-square'"
	:width="`${TOGGLE_SIZE / 2}`"
	:height="`${TOGGLE_SIZE / 2}`"
	viewBox="0, 0, 25, 25"
	xmlns="http://www.w3.org/2000/svg"
>
	<path fill="#000000" d="m6.06542,10.81309c-0.65551,0 -1.18692,0.53138 -1.18692,1.18692c0,0.65553 0.53141,1.18692 1.18692,1.18692l11.86915,0c0.65553,0 1.18692,-0.53138 1.18692,-1.18692c0,-0.65553 -0.53138,-1.18692 -1.18692,-1.18692l-11.86915,0z"/>
	<path fill="#000000" d="m3.09814,0.13085c-1.63879,0 -2.96729,1.3285 -2.96729,2.96729l0,17.80373c0,1.63877 1.3285,2.96729 2.96729,2.96729l17.80373,0c1.63877,0 2.96729,-1.32851 2.96729,-2.96729l0,-17.80373c0,-1.63879 -1.32851,-2.96729 -2.96729,-2.96729l-17.80373,0zm-0.59346,2.96729c0,-0.32775 0.2657,-0.59346 0.59346,-0.59346l17.80373,0c0.32771,0 0.59346,0.2657 0.59346,0.59346l0,17.80373c0,0.32771 -0.26575,0.59346 -0.59346,0.59346l-17.80373,0c-0.32775,0 -0.59346,-0.26575 -0.59346,-0.59346l0,-17.80373z" clip-rule="evenodd" fill-rule="evenodd"/>
</svg>

<!-- Line type: T (├) -->
<svg
	v-if="type === 'T'"
	:width="LINES_SIZE"
	:height="LINES_SIZE"
	:viewBox="`0, 0, ${LINES_SIZE}, ${LINES_SIZE}`"
	x="0"
	y="0"
	xmlns="http://www.w3.org/2000/svg"
>
	<path
		:d="`M${LINES_SIZE / 2 + 1},0 L${LINES_SIZE / 2 + 1},${LINES_SIZE / 2 + 1} L${LINES_SIZE + 0.5},${LINES_SIZE / 2 + 1} M${LINES_SIZE / 2 + 1},${LINES_SIZE / 2 + 1} L${LINES_SIZE / 2 + 1},${LINES_SIZE + 0.5}`"
		fill-opacity="0"
		stroke="#cccccc"
		:stroke-width="LINES_WIDTH"
	/>
</svg>

<!-- Line type: L (└) -->
<svg
	v-if="type === 'L'"
	:width="LINES_SIZE"
	:height="LINES_SIZE"
	:viewBox="`0, 0, ${LINES_SIZE}, ${LINES_SIZE}`"
	x="0"
	y="0"
	xmlns="http://www.w3.org/2000/svg"
>
	<path
		:d="`M${LINES_SIZE / 2 + 1},0 L${LINES_SIZE / 2 + 1},${LINES_SIZE / 2 + 1} L${LINES_SIZE + 0.5},${LINES_SIZE / 2 + 1}`"
		fill-opacity="0"
		stroke="#cccccc"
		:stroke-width="LINES_WIDTH"
	/>
</svg>

<!-- Line type: I (│) -->
<svg
	v-if="type === 'I'"
	:width="LINES_SIZE"
	:height="LINES_SIZE"
	:viewBox="`0, 0, ${LINES_SIZE}, ${LINES_SIZE}`"
	x="0"
	y="0"
	xmlns="http://www.w3.org/2000/svg"
>
	<path
		:d="`M${LINES_SIZE / 2 + 1},0 L${LINES_SIZE / 2 + 1},${LINES_SIZE + 0.5}`"
		fill-opacity="0"
		stroke="#cccccc"
		:stroke-width="LINES_WIDTH"
	/>
</svg>

<!-- Line type: - (─) -->
<svg
	v-if="type === '-'"
	:width="LINES_SIZE"
	:height="LINES_SIZE"
	:viewBox="`0, 0, ${LINES_SIZE}, ${LINES_SIZE}`"
	x="0"
	y="0"
	xmlns="http://www.w3.org/2000/svg"
>
	<path
		:d="`M${LINES_SIZE + 0.5},${LINES_SIZE / 2 + 1} L0,${LINES_SIZE / 2 + 1}`"
		fill-opacity="0"
		stroke="#cccccc"
		:stroke-width="LINES_WIDTH"
	/>
</svg>

<!-- Line type: none (  ) -->
<svg
	v-if="type === 'none'"
	:width="LINES_SIZE"
	:height="LINES_SIZE"
	:viewBox="`0, 0, ${LINES_SIZE}, ${LINES_SIZE}`"
	x="0"
	y="0"
	xmlns="http://www.w3.org/2000/svg"
></svg>

</template>



<script>
export default {
	props: {
		/*modelValue: {
			type: [Number, String],
			default: () => '' 
		},*/
		type: {
			type: String,
			default: () => '',
		},
		linesSize: {
			type: [ String, Number ],
			default: () => 25,
		},
		linesWidth: {
			type: [ String, Number ],
			default: () => 1,
		},
		toggleSize: {
			type: [ String, Number ],
			default: () => 25,
		},
	},
	data() {
		return {
			
		}
	},
	computed: {
		// Local properties
		LINES_SIZE() {
			const match = this.linesSize
				.toString()
				.match( /^\s*(-?\d*\.?\d+)(?:\s*[a-zA-Z%]+)?\s*$/ );
			return match ? parseFloat( match[ 1 ] ) : null;
		},
		LINES_WIDTH() {
			const match = this.linesWidth
				.toString()
				.match( /^\s*(-?\d*\.?\d+)(?:\s*[a-zA-Z%]+)?\s*$/ );
			return match ? parseFloat( match[ 1 ] ) : null;
		},
		TOGGLE_SIZE() {
			const match = this.toggleSize
				.toString()
				.match( /^\s*(-?\d*\.?\d+)(?:\s*[a-zA-Z%]+)?\s*$/ );
			return match ? parseFloat( match[ 1 ] ) : null;
		},
	},
	methods: {
		
	},
	mounted() {
		
	},
}

</script>



<style scoped>



</style>
