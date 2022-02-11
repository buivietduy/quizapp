<template>
	<div class="questions-ctr">
		<div class="progress">
			<div
				class="bar"
				:style="{ width: `${(count / questions.length) * 100}%` }"
			></div>
			<div class="status">
				{{ count }} out of {{ questions.length }} questions answered
			</div>
		</div>
		<transition-group name="fade">
			<div
				class="single-question"
				v-for="(question, index) in questions"
				:key="question.q"
				v-show="count == index"
			>
				<div class="question">{{ question.q }}</div>
				<div class="answers">
					<div
						class="answer"
						v-for="answer in question.answers"
						:key="answer.text"
						@click="selectAnswer(answer.is_correct)"
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
	props: ['questions', 'count'],
	emits: ['send-answer'],
	methods: {
		selectAnswer(result) {
			this.$emit('send-answer', result);
			console.log('Working 1');
		},
	},
};
</script>

<style></style>
