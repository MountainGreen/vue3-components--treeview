# Vue 3 - Component: Treeview

A treeview component that shows hierarichal data as a nested, foldable tree structure. Tree leaves can be selected and make their value available via a `v-model`.


## Installation

__Dependencies__: [Tailwind CSS](https://tailwindcss.com/)

This component with all its subdirectories could be

1) copied into a project's component subdirectory (e.g. `components/Treeview`)
2) used as a submodule inside another Vue 3 project
	```sh
	cd /repos/project
	
	# Add Treeview as a submodule
	mkdir -p ./components/Treeview
	cd ./components/Treeview
	git submodule add <util-methods-url> .
	
	# Commit the changes to the project repository
	cd /repos/project
	git add .
	git commit -m "Added Treeview submodule"
	
	# For later updating the submodule
	cd /repos/project/components/Treeview
	git pull origin main
	
	# To initialize a repository with submodules
	git submodule update --init --recursive --remote
	
	# To update all submodules of a repository later
	git submodule update --recursive --remote
	```
3) used as a subtree inside another Vue 3 project
	```sh
	cd /repos/project

	# Add Treeview as a subtree
	git subtree add --prefix=src/components/Treeview <repo-url> main --squash -m "Added the Treeview component"

	# Change the squash commit message's first line afterwards too if needed
	git filter-branch -f --msg-filter 'sed "s/Squashed.*/{new commit message}/g"' HEAD...HEAD~1
	
	# Pull changes from the Treeview remote repository into the subtree
	git subtree pull --prefix=src/components/Treeview <repo-url> main --squash -m "Updated to the latest Treeview"

	# Push changes that belong to Treeview only to the remote repository (ignoring all changes outside the subtree)
	git subtree push --prefix=src/components/Treeview <repo-url> main
	```
4) installed as a local __NodeJS__ module directly from this GitHub repository


## Caveats when using Git submodules:

- __Updating:__ Submodules do not automatically stay in sync with the remote repository. You need to go into each submodule and pull the changes manually.
- __Committing:__ If you make changes inside a submodule, you need to commit those changes within the submodule first, then go to the main repository and commit the change to the submodule. This is because the main repository tracks the submodule’s commit.
- __Cloning:__ When you clone a repository, the submodules will not be cloned along with it. You need to use `git submodule update --init --recursive` or `git clone --recursive <repository>` to clone the repository and its submodules.
- __Pulling:__ Similarly, when you pull your main repository, it will not pull the new commits of populated submodules. Use the `--recurse-submodules` option with the `git pull` to update all the submodules as well.
- __Cognitive Load:__ When working with submodules, it’s not always clear whether you’re working in the context of your project or one of its dependencies. This can increase the cognitive load and complexity of your project.


## Usage

```vue
<template>

	<Treeview />

</template>

<script>
import Treeview from './components/Treeview/Treeview.vue'


export default {
	components: {
		Treeview,
	},
	methods: {
		
	}
}
</script>
```

