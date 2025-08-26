<template>

<div class="p-4 text-sm font-mono text-gray-800">
	<h2 class="mb-2 font-bold">Project Structure</h2>
	<treeview-tree
		v-model:currentPath="currentPath"
		v-model:descendantPaths="descendantPaths"
		:data="jsonData"
	/>
</div>
<p>{{ currentPath }}</p>
<p>{{ descendantPaths }}</p>

</template>



<script>
// Components
import TreeviewTree from "./modules/Treeview-Tree.vue"

export default {
	name: 'Treeview',
	props: {
		type: {
			type: String,
			default: '',
		},
	},
	components: {
		TreeviewTree,
	},
	directives: {
	},
	data() {
		return {
			jsonData: {
				'src.js': {
					components: {
						'Header.vue': null,
						'Footer.vue': null,
					},
					'App.vue': null,
					'main.js': null,
				},
				public: {
					'index.html': null,
					'favicon.ico': null,
				},
				'package.json': null
			},
			
			currentPath: null,
			descendantPaths: [],
		}
	},
	computed: {
		
	},
	methods: {
		
	},
}

</script>



<style scoped>



</style>
	
