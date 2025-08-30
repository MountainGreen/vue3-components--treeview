<template>

<li class="leading-snug">
	<div
		class="flex items-center font-mono text-sm cursor-pointer select-none leading-[1.2] hover:text-blue-600"
		@click.stop="toggle"
	>
		<!-- Tree lines (└ , ├ etc) -->
		<treeview-icon
			v-for="line in prefix"
			:type="line"
			:lines-size="linesSize"
			:lines-width="linesWidth"
		/>
		
		<!-- Expandable / collapsable sign -->
		<span v-if="isObject" :style="{ width: linesSize }" class="flex justify-center items-center mr-1 font-bold text-gray-600">
			<span v-if="toggleChar" class="node-fontsize">{{ expanded ? '−' : '+' }}</span>
			<treeview-icon v-if="! toggleChar && expanded" type="minus-square" />
			<treeview-icon v-else-if="! toggleChar && ! expanded" type="plus-square" />
		</span>
		<span v-else :style="{ width: linesSize }" class="mr-1"></span>
		
		<!-- Node label -->
		<span
			:class="[
				'text-gray-800 text-[',
				{
					'ml-[-0.9rem]': ! isObject,
					'bg-primary-300 rounded px-1': selected === currentPath,
				},
			]"
			@click.stop="handleClick"
		>
			{{ label }}
		</span>
	</div>
	
	<ul v-if="isObject && expanded">
		<treeview-node
			v-for="( childValue, index ) in Object.values( value )"
			:key="Object.keys( value )[ index ]"
			:label="Object.keys( value )[ index ]"
			:value="childValue"
			:path="[ ...path, label ]"
			:depth="depth + 1"
			:is-last="index === Object.keys( value ).length - 1"
			:ancestors="ancestorsWithThis"
			:selected="selected"
			@node-click="emitNodeClick"
		/>
	</ul>
</li>

</template>



<script>
// Components
import TreeviewIcon from "./Treeview-Icon.vue"

export default {
	name: 'TreeviewNode',
	props: {
		/*modelValue: {
			type: [ Number, String ],
			default: () => '' 
		},*/
		label: String,
		value: [ Object, null ],
		path: {
			type: Array,
			default: () => [],
		},
		depth: {
			type: Number,
			default: 0,
		},
		isLast: {
			type: Boolean,
			default: false,
		},
		ancestors: {
			type: Array,
			default: () => [],
		},
		selected: {
			type: [ String, null ],
			default: () => null,
		},
		
		// Options
		toggleChar: {
			type: Boolean,
			default: () => false,
		},
		linesSize: {
			type: String,
			default: () => '25px',
		},
		linesWidth: {
			type: [ String, Number ],
			default: () => 1,
		},
		fontSize: {
			type: String,
			default: () => '14px',
		},
	},
	components: {
		TreeviewIcon,
	},
	emit: [
		//'update:modelValue',
		'node-click',
	],
	watch: {
		/*modelValue( newValue ) {
			this.$emit( 'update:modelValue', newValue );
		},*/
	},
	data() {
		return {
			expanded: true,
		}
	},
	computed: {
		isObject() {
			return typeof this.value === 'object' && this.value !== null;
		},
		ancestorsWithThis() {
			return [ ...this.ancestors, ! this.isLast ];
		},
		prefix() {
			const parts = this.ancestors.map( showLine => showLine ? 'I' : 'none' );
			parts.push( this.isLast ? 'L' : 'T' );
			return parts;
		},
		
		currentPath() {
			const fullPath = [ ...this.path, this.label ];
			return this.formatPath( fullPath );
		},
	},
	methods: {
		toggle() {
			if ( this.isObject ) {
				this.expanded = ! this.expanded;
			}
		},
		
		handleClick( e ) {
			const fullPath = [ ...this.path, this.label ];
			const currentPath = this.formatPath( fullPath );
			const childrenPaths = this.isObject
				? this.getDescendantPaths( this.value, fullPath )
				: [];
			
			this.$emit( 'node-click', {
				path: currentPath,
				children: childrenPaths,
			} )
		},
		
		getDescendantPaths( obj, basePath = [] ) {
			// Recursively collect all descendant paths in dot notation
			const paths = []
			
			for ( const key in obj ) {
				const value = obj[ key ];
				const current = [ ...basePath, key ];
				
				if ( value && typeof value === 'object' ) {
					paths.push( ...this.getDescendantPaths( value, current ) );
				} else {
					paths.push( this.formatPath( current ) );
				}
			}
			
			return paths;
		},
		
		// Safe formatter for dot+bracket notation
		formatPath( segments ) {
			return segments
				.map( ( key ) => {
					const isSafe = /^[a-zA-Z_$][\w$]*$/.test( key )
					return isSafe ? `.${ key }` : `["${ key }"]`
				})
				.join( '' )
				.replace( /^\./, '' ) // strip first dot
		},
		
		emitNodeClick( payload ) {
			this.$emit( 'node-click', payload );
		},
	},
	mounted() {
		
	},
}

</script>



<style scoped>



</style>
