<template>
	<div class="QuestionControler">
		<div class="Progress">
			<div
				class="Bar"
				:style="{ width: `${(counts / questions.length) * 100}%` }"
			></div>
			<div class="Status">
				{{ questions.length }}つの質問のうち{{ counts }}が回答されました
			</div>
		</div>
		<transition-group name="fade">
			<div
				class="SingleQuestion"
				v-for="(question, index) in questions"
				:key="question.q"
				v-show="counts == index"
			>
				<div class="Question">{{ question.q }}</div>
				<div class="Answers">
					<div
						class="Answer"
						v-for="(answer, ansindex) in question.answers"
						:key="answer.text"
						@click="selectAnswer(answer.is_correct, ansindex)"
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
	props: ['questions', 'counts'],
	emits: ['send-answer'],
	methods: {
		selectAnswer(result, index) {
			//Emmiting Event to the Root component and send correct or not and the index user choose
			this.$emit('send-answer', result, index);
		},
	},
};
</script>

<style></style>
