<template>
<div>
    <div v-for="(option, index) in question.choices">
        <div class="input">
        <input @change="saveAnswer" type="checkbox" :id="'q'+index" :name="'q'+index" v-model="answers" :value="index"/>
        <label :for="'q'+index">
            {{ option.text }}
        </label>
        </div>
    </div>
    <div v-if="review">
        Score: {{ score }}
    </div>
</div>
</template>

<script>

export default {
    props: ['question', 'review'],
    data: function() {
        return {
            answers: (this.question.savedAnswer) ? JSON.parse(this.question.savedAnswer) : []
        }
    },

    watch: {
        question: function () {
            this.answers = (this.question.savedAnswer) ? JSON.parse(this.question.savedAnswer) : []
        }
    },

    computed: {
        answer: function() {
            return JSON.stringify(this.answers.sort())
        },

        score: function() {
            let score = 0
            let answers  = JSON.parse(this.question.savedAnswer)

            for (let i=0; i < this.question.choices.length; i++) {
                if (answers.includes(i)) {
                    score += this.question.choices[i].score
                }
            }
            return score
        }
    },


    methods: {
        saveAnswer() {
            this.$emit('saved', this.answer)
	}
    }
}
</script>


<style scoped>
.input  {
    width: 100%;
    padding: 0 0 0 5px;
    border-radius: 5px;
    background: #f4f4f4;
    cursor: pointer;
    margin-bottom: 0.5em;
    display: flex;
    border: 1px solid #ccc;
}

label {
    padding: 5px;
    width: 100%;
}

label:hover {
    background: #ccc;
}

input {
justify-content: center;
text-align: center;
}

input[type="checkbox"] {
    display: flex;
    align-items: center;
    margin: auto 10px auto 5px;
}

label {
    border-left: 1px solid #ccc;
}

input:checked {
    background: #a7cf5f;
    background: #679436;
    color: #fff;
    border: 1px solid red;
}

input:checked + label {
    background: #a7cf5f;
    background: #679436;
    color: #fff;
}

label {
    position: relative;
}
</style>
