<template>
	<div class="Result">
		<div class="Title">{{ results[checkResult].title }}</div>
		<div class="Description">{{ results[checkResult].desc }}</div>
		<button
			type="button"
			class="ReviewBtn"
			@click.prevent="review = !review"
		>
			Review
		</button>
		<transition-group name="fade">
			<div
				class="ReviewQuestion"
				v-for="(question, index) in questions"
				:key="question.q"
				v-show="review"
			>
				<div class="QuestionReview">{{ question.q }}</div>
				<div class="AnswersReview">
					<div
						class="AnswerReview"
						v-for="(answer, ai) in question.answers"
						:key="answer.text"
						:style="[
							{ 'background-color': backgroundColor(index, ai) },
							{ color: color(index, ai) },
						]"
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
	props: ['results', 'corrects', 'questions', 'answerchooses'],
	data() {
		return {
			review: false,
		};
	},
	methods: {
		backgroundColor(index, ai) {
			//Change the background color,green for the correct answer, red for the answer user choose and not correct
			return this.questions[index].answers[ai].is_correct
				? '#8ce200'
				: this.answerchooses[index] == ai
				? 'red'
				: '';
		},
		color(index, ai) {
			//Change the text color,white for the correct answer and the answer user choose and not correct
			return this.questions[index].answers[ai].is_correct ||
				this.answerchooses[index] == ai
				? '#fff'
				: '';
		},
	},
	computed: {
		checkResult() {
			//check the result to take the index of the title and the description
			let i = 0;
			this.results.forEach((item, index) => {
				if (item.min <= this.corrects && item.max >= this.corrects)
					i = index;
			});
			return i;
		},
	},
};
</script>

<style></style>
