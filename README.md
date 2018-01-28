vue-pagination-simple
=============

Simple pagination vue component

## Installation
---------------
### npm
``` sh
npm install --save vue-pagination-simple
```

## Usage
---------------

```vue
<template>
	<div>
		<app-pagination class="center"
			:current="currentPage" 
			:total="totalPages" 
			:per-page="perPage"
			:active-color="'#007DFF'"
			:active-font-color="'black'"
			@page-changed="changePage"
		></app-pagination>
	</div>
</template>

<script>
export default {
	name: 'app',
	data () {
		return {
			currentPage: 6,
			totalPages: 10,
			pageRange: 3
		}
	},
	methods: {
		changePage(page) {
			console.log(`page changed on ${page}`);
			this.currentPage = page;
		}
	}
}
</script>

<style scoped>

// you can add style of pagination hover and border by class .pagination

.pagination a:hover:not(.active) {
	background-color: #ddd;
}

.pagination a {
	border: 1px solid #ddd;
}

.center {
  display: flex;
  justify-content: center;
}

</style>

```