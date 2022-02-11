<template>
	<div class="questions-ctr">
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
export default {};
</script>

<style></style>
