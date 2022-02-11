<template>
	<div class="Controler">
		<transition name="fade" mode="out-in">
			<question
				v-if="counts < questions.length"
				:questions="questions"
				:counts="counts"
				@send-answer="receiver"
			/>
			<result
				v-else
				:results="results"
				:corrects="corrects"
				:questions="questions"
				:answerchooses="answerchooses"
			/>
		</transition>
		<button type="button" class="ResetBtn" @click.prevent="reset">
			Reset
		</button>
	</div>
</template>

<script>
import Question from './components/Question.vue';
import Result from './components/Result.vue';

export default {
	name: 'App',
	data() {
		return {
			counts: 0,
			corrects: 0,
			answerchooses: [],
			questions: [
				{
					q: '君＿どこ＿ですか',
					answers: [
						{
							text: 'は／に',
							is_correct: true,
						},
						{
							text: 'の／に',
							is_correct: false,
						},
						{
							text: 'は／の',
							is_correct: false,
						},
						{
							text: 'の／は',
							is_correct: false,
						},
					],
				},
				{
					q: '後で',
					answers: [
						{
							text: 'つぎ',
							is_correct: false,
						},
						{
							text: 'うしろ',
							is_correct: false,
						},
						{
							text: 'あと',
							is_correct: true,
						},
						{
							text: 'まえ',
							is_correct: false,
						},
					],
				},
				{
					q: '三＋七＝？',
					answers: [
						{
							text: '百',
							is_correct: false,
						},
						{
							text: '十',
							is_correct: true,
						},
						{
							text: '万',
							is_correct: false,
						},
					],
				},
			],
			results: [
				{
					min: 0,
					max: 2,
					title: 'リトライ!',
					desc: '頑張ってね!',
				},
				{
					min: 3,
					max: 3,
					title: 'すごいいだね！',
					desc: '学習は良いです!',
				},
			],
		};
	},
	methods: {
		receiver(result, index) {
			// Check if the user choose the correct answer or not, and save the user input
			this.answerchooses.push(index);
			if (result) {
				this.corrects++;
			}
			this.counts++;
		},
		reset() {
			// Reset the Quiz
			this.counts = 0;
			this.corrects = 0;
			this.answerchooses = [];
		},
	},
	components: {
		Question,
		Result,
	},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
