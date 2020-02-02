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
            <page-component>
                <p>
                    You have finished the quiz. Do you want to review the questions?
                </p>
		<div class="flex justify-end mt-8">
   		    <button @click="reviewQuestions"
			    class="flex justify-end bg-blue-700 hover:bg-blue-500 text-white font-bold py-2 px-4 rounded">
                        <span>Review</span>
		    </button>
                 </div>
            </page-component>
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

import PageComponent from './PageComponent'
import QuestionComponent from './QuestionComponent'

import questions from './questions.json'


export default {

    components: {
        QuestionComponent,
        PageComponent
    },
    data: function() {
	return {
    	    questions: questions,
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
        console.log('Quiz component mounted.')
    }
}
</script>
