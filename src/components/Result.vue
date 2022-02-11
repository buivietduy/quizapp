<template>
	<div class="result">
		<div class="title">{{ results[checkResult].title }}</div>
		<div class="desc">{{ results[checkResult].desc }}</div>
		<button
			type="button"
			class="reset-btn"
			@click.prevent="review = !review"
		>
			Review
		</button>
		<transition-group name="fade">
			<div
				class="review-question"
				v-for="(question, index) in questions"
				:key="question.q"
				v-show="review"
			>
				<div class="question-review">{{ question.q }}</div>
				<div class="answers-review">
					<div
						class="answer-review"
						v-for="(answer, ai) in question.answers"
						:key="answer.text"
						:style="{ 'background-color': backgroundColor(index, ai) }"
					>
						{{ answer.text }}
					</div>
				</div>
			</div>
		</transition-group>
	</div>
</template>

<script>
export default {
	props: ['results', 'correct', 'questions', 'answerchoose'],
	data() {
		return {
			review: false,
		};
	},
	methods: {
		backgroundColor(index, ai) {
			return this.questions[index].answers[ai].is_correct
				? '#8ce200'
				: this.answerchoose[index] == ai
				? 'red'
				: '';
		},
	},
	computed: {
		checkResult() {
			console.log(this.answerchoose);
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
