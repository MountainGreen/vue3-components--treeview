<template>

<!-- Plus squared -->
<svg v-if="type === 'plus-square'" width="12px" height="12px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path d="M12 6C12.5523 6 13 6.44772 13 7V11H17C17.5523 11 18 11.4477 18 12C18 12.5523 17.5523 13 17 13H13V17C13 17.5523 12.5523 18 12 18C11.4477 18 11 17.5523 11 17V13H7C6.44772 13 6 12.5523 6 12C6 11.4477 6.44772 11 7 11H11V7C11 6.44772 11.4477 6 12 6Z" fill="#000000"></path> <path fill-rule="evenodd" clip-rule="evenodd" d="M2 4.5C2 3.11929 3.11929 2 4.5 2H19.5C20.8807 2 22 3.11929 22 4.5V19.5C22 20.8807 20.8807 22 19.5 22H4.5C3.11929 22 2 20.8807 2 19.5V4.5ZM4.5 4C4.22386 4 4 4.22386 4 4.5V19.5C4 19.7761 4.22386 20 4.5 20H19.5C19.7761 20 20 19.7761 20 19.5V4.5C20 4.22386 19.7761 4 19.5 4H4.5Z" fill="#000000"></path> </g></svg>

<!-- Minus squared -->
<svg v-if="type === 'minus-square'" width="12px" height="12px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path d="M7 11C6.44772 11 6 11.4477 6 12C6 12.5523 6.44772 13 7 13H17C17.5523 13 18 12.5523 18 12C18 11.4477 17.5523 11 17 11H7Z" fill="#000000"></path> <path fill-rule="evenodd" clip-rule="evenodd" d="M4.5 2C3.11929 2 2 3.11929 2 4.5V19.5C2 20.8807 3.11929 22 4.5 22H19.5C20.8807 22 22 20.8807 22 19.5V4.5C22 3.11929 20.8807 2 19.5 2H4.5ZM4 4.5C4 4.22386 4.22386 4 4.5 4H19.5C19.7761 4 20 4.22386 20 4.5V19.5C20 19.7761 19.7761 20 19.5 20H4.5C4.22386 20 4 19.7761 4 19.5V4.5Z" fill="#000000"></path> </g></svg>

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
	},
	methods: {
		
	},
	mounted() {
		
	},
}

</script>



<style scoped>



</style>
