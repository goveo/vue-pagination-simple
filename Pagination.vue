<template id="pagination-template">
	<div class="pagination">
		<div class="center">
			<a :style="notActiveStyle" href="#" v-if="hasPrev()" @click.prevent="changePage(prevPage)">Prev</a>
			<span v-if="hasFirst()"><a href="#" :style="notActiveStyle"  @click.prevent="changePage(1)">1</a></span>
			<a :style="notActiveStyle" v-if="hasFirstDots()">...</a>
			<span v-for="page in pages" :key="page">
				<a v-if="page == current" class="active" :style="activeStyle" href="#" @click.prevent="changePage(page)">
					{{ page }}
				</a>
				<a :style="notActiveStyle" v-else href="#" @click.prevent="changePage(page)">
					{{ page }}
				</a>
			</span>
			<a :style="notActiveStyle" v-if="hasLastDots()">...</a>
			<span v-if="hasLast()"><a href="#" :style="notActiveStyle"  @click.prevent="changePage(total)">{{ total }}</a></span>

			<a :style="notActiveStyle" href="#" v-if="hasNext()" @click.prevent="changePage(nextPage)">Next</a>
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
		},
		color: {
			type: String,
			default: "white"
		},
		fontColor: {
			type: String,
			default: "black"
		},
		activeFontColor: {
			type: String,
			default: "white"
		},
		activeColor: {
			type: String,
			default: "#007DFF"
		},
		borderColor: {
			type: String,
			default: "#ddd"
		}
	},
	computed: {
		pages: function () {
			let pages = [];

			for (let i = this.rangeStart; i <= this.rangeEnd; i++) {
				pages.push(i);
			}

			return pages;
		},
		rangeStart: function () {
			let start = this.current - this.pageRange;

			if (start > 0) {
				return start;
			} else {
				return 1;
			}
			// return (start > 0) ? start : 1;
		},
		rangeEnd: function () {
			let end = this.current + this.pageRange;

			return (end < this.total) ? end : this.total;
		},
		nextPage: function () {
			return this.current + 1;
		},
		prevPage: function () {
			return this.current - 1;
		},
		activeStyle: function() {
			return {
				color: this.activeFontColor,
				backgroundColor: this.activeColor,
				border: `1px solid ${this.borderColor}`,
			}
		},
		notActiveStyle: function() {
			return {
				color: this.fontColor,
				backgroundColor: this.color,
				border: `1px solid ${this.borderColor}`
			}
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
		}
	}
}
</script>

<style scoped>

.pagination {
    display: inline-block;
	margin-top: 20px;
}

a {
    color: black;
    float: left;
    padding: 8px 16px;
    text-decoration: none;
    transition: background-color .3s;
}

a:hover:not(.active) {
	background-color: greenyellow;
}

.center {
  display: flex;
  justify-content: center;
}

</style>
