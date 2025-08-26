<template>

<ul class="text-sm font-mono text-gray-800">
	<treeview-node
		v-for="( value, key, index ) in data"
		:key="key"
		:label="key"
		:value="value"
		:path="[]"
		:depth="0"
		:is-last="index === Object.keys(data).length - 1"
		:ancestors="[]"
		:selected="currentPath"
		@node-click="handleNodeClick"
	/>
</ul>

</template>



<script>
// Components
import TreeviewNode from "./Treeview-Node.vue"

export default {
	props: {
		/*modelValue: {
			type: [Number, String],
			default: () => '' 
		},*/
		currentPath: {
			type: [ String, null ],
			default: () => null,
		},
		descendantPaths: {
			type: Array,
			default: () => [],
		},
		data: {
			type: Object,
			required: true,
		},
	},
	components: {
		TreeviewNode,
	},
	directives: {
	},
	emit: [
		//'update:modelValue',
		'update:currentPath',
		'update:descendantPaths',
	],
	watch: {
		/*modelValue( newValue ) {
			this.$emit( 'update:modelValue', newValue );
		},*/
	},
	data() {
		return {
			
		}
	},
	computed: {
		
	},
	methods: {
		handleNodeClick( { path, children } ) {
			this.$emit( 'update:currentPath', path );
			this.$emit( 'update:descendantPaths', children );
			
			console.log( 'Clicked path:', path );
			console.log( 'Descendant paths:', children );
		},
	},
	mounted() {
		
	},
}

</script>



<style scoped>



</style>
