<template>
    <div class="mt-12 max-w-xl mx-auto flex flex-col">
        <h1 class="text-center text-xl mb-12">Quiz</h1>

        <!--
        <div>
            Time: {{ timeLeft }}
        </div>
        -->


        <div v-if="!done">
            <question-component
                :total="questions.length"
                :review="review"
                :question="questions[currQuestion]">
            </question-component>
        </div>
        <div v-else>
            <page-component>
                <p>
                    You have finished the quiz. Do you want to review the questions?
                </p>
		<div class="flex mt-8">
   		    <button @click="clearAnswers"
			    class="flex justify-start bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded">
                        <span>Clear answers</span>
		    </button>
                 </div>
		<div class="flex justify-end mt-8">
   		    <button @click="reviewQuestions"
			    class="flex justify-end bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded">
                        <span>Review</span>
		    </button>
                 </div>
            </page-component>
        </div>

        <div v-if="!done" class="flex justify-between mt-8">
            <button v-if="canBackTrack" @click="prevQuestion"
                class="bg-gray-700 hover:bg-gray-800 text-white font-bold py-2 px-4 rounded">
                <span>Prev</span>
            </button>
            <div v-else></div>

            <button @click="nextQuestion"
                class="bg-gray-700 hover:bg-gray-800 text-white font-bold py-2 px-4 rounded">
                <span>Next</span>
            </button>
	</div>
    </div>
</template>

<script>

import PageComponent from './PageComponent'
import QuestionComponent from './QuestionComponent'

import questionsData from './questions.json'


export default {

    components: {
        QuestionComponent,
        PageComponent
    },
    data: function() {
	return {
	    currQuestion: 0,
	    done: false,
            review: false,
            durationPerQuestion: 10,
            canBackTrack: true,
            timeLeft: this.testDuration
	}
    },

    methods: {
        clearAnswers() {
            localStorage.clear()
        },

        nextQuestion() {
	    if (this.currQuestion < this.questions.length) {
		this.currQuestion++
	    }

	    if (this.currQuestion == this.questions.length) {
	        this.done = true
	    }
	},

        prevQuestion() {
	    if (this.currQuestion > 0) {
		this.currQuestion--
	    }
	},

        reviewQuestions() {
            this.currQuestion = 0
            this.done = false
            this.review = true
        },

        countDownTimer() {
            if(this.timeLeft > 0) {
                setTimeout(() => {
                    this.timeLeft -= 1
                    this.countDownTimer()
                }, 1000)
            } else {
                if (!this.done) {
                this.nextQuestion()
                this.timeLeft = this.durationPerQuestion
                this.countDownTimer()
                }
            }
        }
    },

    computed: {
        questions: function() {
            let i = 1
            return questionsData.map(function(item) {
                item.id = i++
                return item
            })
        }
    },

    created() {
       //this.countDownTimer()
    },

    mounted() {
        console.log('Quiz component mounted.')
    }
}

//https://stackoverflow.com/questions/55773602/how-do-i-create-a-simple-10-seconds-countdown-in-vue-js

</script>
