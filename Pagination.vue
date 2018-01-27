<template id="pagination-template">
	<div class="pagination">
		<div class="center">
			<a href="#" v-if="hasPrev()" @click.prevent="changePage(prevPage)">Prev</a>
			<span v-if="hasFirst()"><a href="#" @click.prevent="changePage(1)">1</a></span>
			<a v-if="hasFirstDots()">...</a>
			<span v-for="page in pages" :key="page">
				<a v-if="page == current" class="active" href="#" @click.prevent="changePage(page)">
					{{ page }}
				</a>
				<a v-else href="#" @click.prevent="changePage(page)">
					{{ page }}
				</a>
			</span>
			<a v-if="hasLastDots()">...</a>
			<span v-if="hasLast()"><a href="#" @click.prevent="changePage(total)">{{ total }}</a></span>

			<a href="#" v-if="hasNext()" @click.prevent="changePage(nextPage)">Next</a>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		current: {
			type: Number,
			default: 1
		},
		total: {
			type: Number,
			default: 0
		},
		pageRange: {
			type: Number,
			default: 2
		}
	},
	computed: {
		pages: function () {
			var pages = [];

			for (var i = this.rangeStart; i <= this.rangeEnd; i++) {
				pages.push(i);
			}

			return pages;
		},
		rangeStart: function () {
			var start = this.current - this.pageRange;

			return (start > 0) ? start : 1;
		},
		rangeEnd: function () {
			var end = this.current + this.pageRange;

			return (end < this.total) ? end : this.total;
		},
		nextPage: function () {
			return this.current + 1;
		},
		prevPage: function () {
			return this.current - 1;
		}
	},
	methods: {
		hasFirst: function () {
			return this.rangeStart !== 1;
		},
		hasLast: function () {
			return this.rangeEnd < this.total;
		},
		hasFirstDots: function () {
			if (this.rangeStart <= 2) {
				return false; 
			} else {
				return true;
			}
		},
		hasLastDots: function () {
			console.log('this.rangeEnd : ', this.rangeEnd)
			console.log('this.total - 1 : ', this.total - 1)
			if (this.rangeEnd >= this.total - 1) {
				return false; 
			} else {
				return true;
			}
		},
		hasPrev: function () {
			return this.current > 1;
		},
		hasNext: function () {
			return this.current < this.total;
		},
		changePage: function (page) {
			this.$emit('page-changed', page);
		},
		created: function() {
			console.log('pagination created');
		}
	}
}
</script>

<style>

.pagination {
    display: inline-block;
	margin-top: 20px;
}

.pagination a {
    color: black;
    float: left;
    padding: 8px 16px;
    text-decoration: none;
    transition: background-color .3s;
    border: 1px solid #ddd;
}

.pagination a.active {
    background-color: #007DFF;
    color: white;
    border: 1px solid #007DFF;
}

.pagination a:hover:not(.active) {
	background-color: #ddd;
}

.center {
  display: flex;
  justify-content: center;
  /* align horizontal */
}

</style>
