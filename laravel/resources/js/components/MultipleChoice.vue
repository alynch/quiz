<template>
<div>
    <div v-for="(option, index) in question.choices">
        <div class="input">
            <input @change="saveAnswer" type="radio" :id="'q'+index" v-model="answer" name="q" :value="index"/>
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
            answer: this.question.savedAnswer
        }
    },

    watch: {
        question: function () {
            this.answer = this.question.savedAnswer
        }
    },

    computed: {
        score: function() {
            if (this.question.savedAnswer) {
                return this.question.choices[this.question.savedAnswer].score
            } else {
                return 0;
            }
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

input[type="radio"] {
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
</style>
