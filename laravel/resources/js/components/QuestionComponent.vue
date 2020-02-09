<template>
    <div style="position:relative" class="p-6 bg-white rounded-lg shadow-xl">
        <div class="question-number">
            {{ question.id }} / {{ total }}
        </div>

        <h4 class="text-lg text-gray-900 mb-6">
            {{ question.title }}
        </h4>
        <p class="text-gray-800">
            {{ question.prompt }}
        </p>

        <component v-bind:is="currentType"
            :question="this.question"
            :review="review"
            @saved="saveAnswer">
        </component>
    </div>
</template>

<script>
import MultipleChoice from './MultipleChoice'
import CheckBox from './CheckBox'
import Input from './Input'
import Sort from './Sort'

export default {
    components: {
        MultipleChoice,
        CheckBox,
        Input,
        Sort
    },

    props: ['total', 'question', 'review'],

 	data: function() {
            return {
                currentView: null,
                savedAnswer: null
            }
	},

        computed: {
            currentType: function() {
                if (this.question.type == 'radio') {
                    return MultipleChoice
                } else if (this.question.type == 'checkbox') {
                    return CheckBox
                } else if (this.question.type == 'input') {
                    this.question.options = this.question.prompt
                    return Input
                } else if (this.question.type == 'sort') {
                    return Sort
                }
            },

            saved: function() {
                return localStorage.getItem('q.' + this.question.id)
            }
        },

        methods: {
            saveAnswer(answer) {
                localStorage.setItem('q.' + this.question.id, answer);
	    }
        },

        watch: {
            question: function (val) {
                this.question.savedAnswer = localStorage.getItem('q.' + this.question.id)
                //this.answer = null
            }    
        },

        created() {
            this.question.savedAnswer = localStorage.getItem('q.' + this.question.id)
        },

        updated() {
            this.question.savedAnswer = localStorage.getItem('q.' + this.question.id)
        },

	mounted() {
            console.log('Question component mounted.')
        }
    }
</script>


<style>
.question-number {
	background: #ffffff;
	color: #6a6a6a;
	border: 1px solid #dedede;
	border-radius: 5px;
	box-shadow: 0 1px 3px rgba(0, 0, 0, 0.25);
	padding: 5px;
	position: absolute;
	top: 2em;
	right: -3em;
	width: 4em;
	margin-left: 1em;
	text-align: center;
}

label {
    display: block;
    width: 100%;
    padding: 5px;
    border-radius: 5px;
    background: #f4f4f4;
    cursor: pointer;
}

label:hover {
    background: #a7cf5f;
    background: #66aa66;
    background: #679436;
    background: #74a73d;
}

input[type=radio], input[type=checkbox] {
     margin-left: -1000px;
}

</style>
