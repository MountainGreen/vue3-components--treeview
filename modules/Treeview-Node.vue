<template>

<li class="leading-snug">
	<div
		class="flex items-center font-mono text-sm cursor-pointer select-none leading-[1.2] hover:text-blue-600"
		@click.stop="toggle"
	>
		<!-- Tree bar structures as utf8-characters (└── , ├── etc) -->
		<span class="whitespace-pre text-gray-500 lines-fontsize lines-margin-y">
			{{ prefix }}
		</span>
		
		<!-- Expandable / collapsable sign -->
		<span v-if="isObject" class="w-4 text-center mr-1 font-bold text-gray-600">
			<span v-if="toggleChar" class="node-fontsize">{{ expanded ? '−' : '+' }}</span>
			<treeview-icon v-if="! toggleChar && expanded" type="minus-square" />
			<treeview-icon v-else-if="! toggleChar && ! expanded" type="plus-square" />
		</span>
		<span v-else class="w-4 mr-1"></span>
		
		<!-- Node label -->
		<span
			:class="[
				'text-gray-800 node-fontsize',
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
			const parts = this.ancestors.map( showLine => showLine ? '│   ' : '    ' );
			parts.push( this.isLast ? '└── ' : '├── ' );
			return parts.join( '' );
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

.lines-fontsize {
	font-size: calc( 1.5 * v-bind( fontSize ) );
}
.lines-margin-y {
	margin-top: calc( -1 * 1.5 * v-bind( fontSize ) / 7 );
	margin-bottom: calc( -1 * 1.5 * v-bind( fontSize ) / 7 );
}

.node-fontsize {
	font-size: v-bind( fontSize );
}

</style>
