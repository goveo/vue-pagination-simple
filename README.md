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

```html
<template>
	<div>
		<app-pagination class="center"
    		:current="currentPage" 
    		:total="totalPages" 
    		:page-range="pageRange"
    		:active-font-color="'black'"
    		:active-color="'#007DFF'"
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
			pageRange: 2
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
## Example
---------------

<img src="https://i.imgur.com/y9LgCDm.jpg" alt="pagination example"></img>