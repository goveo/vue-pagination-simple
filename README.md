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
		<app-pagination
			:current="currentPage"
			:total="totalPages"
			:page-range="pageRange"
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
	}
}
</script>
```