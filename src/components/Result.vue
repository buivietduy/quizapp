<template>
	<div class="result">
		<div class="title">{{ results[checkResult].title }}</div>
		<div class="desc">{{ results[checkResult].desc }}</div>
	</div>
</template>

<script>
export default {
	props: ['results', 'correct'],
	computed: {
		checkResult() {
			let i = 0;
			this.results.forEach((item, index) => {
				if (item.min <= this.correct && item.max >= this.correct)
					i = index;
			});
			return i;
		},
	},
};
</script>

<style></style>
