<template>
    <div class="mt-12 max-w-lg mx-auto flex flex-col">
        <h1 class="text-center text-xl">Quiz</h1>

   
        <div v-if="!done">
            <question-component
                :id="curr_question+1"
                :total="questions.length"
                :question="questions[curr_question]">
            </question-component>
        </div>
        <div v-else>
            <p>
                You have finished the quiz. Do you want to review the questions?
            </p>
		    <div class="flex justify-end mt-8">
   		    <button @click="reviewQuestions"
			    class="flex justify-end bg-blue-700 hover:bg-blue-500 text-white font-bold py-2 px-4 rounded">
                <span>Review</span>
		    </button>
         </div>
     </div>

		<div class="flex justify-end mt-8">
            <div v-if="!done">
		    <button @click="nextQuestion"
			    class="flex justify-end bg-blue-700 hover:bg-blue-500 text-white font-bold py-2 px-4 rounded">
                <span>Next</span>
		    </button>
            </div>
		</div>
    </div>
</template>

<script>

import QuestionComponent from './QuestionComponent'

export default {

    components: {
        QuestionComponent
    },
	data: function() {
	return {
    	questions: [
			{
				'title': 'Question 1',
				'prompt': 'How do you implement an efficent sort algorithm?',
                'type': 'radio',
                'options': [
                    'Do a binary search',
                    'Just use bubble sort!'
                ]
			},
			{
				'title': 'Question 2',
				'prompt': 'What is the difference between "==" and "===" in PHP?',
                'type': 'radio',
                'options': [
                    'They are the same',
                    'One is better than the other one'
                ]
			},
			{
				'title': 'Question 3',
				'prompt': 'Whas is the difference beween an "id" and a "class" in CSS?',
                'type': 'radio',
                'options': [
                    '"id" is more efficient',
                    '"id" does not work on IE',
                    'All of the above'
                ]
			},
			{
				'title': 'Question 4',
				'prompt': 'Which of these are valid HTTP methods?',
                'type': 'checkbox',
                'options': [
                    'OPTIONS, GET, HEAD, POST',
                    'OPTIONS, GET, HEAD, POST, PUT, PATCH',
                    'HEAD, OPTIONS, GET, HEAD, POST, PUT, PATCH',
                ]
			},
			{
				'title': 'Question 5',
				'prompt': 'How do you initialize a repostitory in git?',
                'type': 'radio',
                'options': [
                    'git commit master',
                    'git init --bare',
                    'git init'
                ]
			},
		],
		curr_question: 0,
		done: false,
        review: false
		}
	},
	 methods: {
            nextQuestion() {
				if (this.curr_question < this.questions.length) {
					this.curr_question++
				}

				if (this.curr_question == this.questions.length) {
					this.done = true
				}
			},
            reviewQuestions() {
                this.curr_question = 0
                this.done = false
                this.review = true
			}
	},

	mounted() {
            console.log('Component mounted.')
        }
    }

</script>
