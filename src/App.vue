<template>
	<div class="ctr">
		<transition name="fade" mode="out-in">
			<question
				v-if="count < questions.length"
				:questions="questions"
				:count="count"
				@send-answer="receiver"
			/>
			<result
				v-else
				:results="results"
				:correct="correct"
				:questions="questions"
				:answerchoose="answerchoose"
			/>
		</transition>
		<button type="button" class="reset-btn" @click.prevent="reset">
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
			count: 0,
			correct: 0,
			answerchoose: [],
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
			this.answerchoose.push(index);
			if (result) {
				this.correct++;
			}
			this.count++;
		},
		reset() {
			this.count = 0;
			this.correct = 0;
			this.answerchoose = [];
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
