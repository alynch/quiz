<template>
<div>
    <div v-for="(option, index) in question.choices">
        <input @change="saveAnswer" type="radio" :id="'q'+index" v-model="answer" name="q" :value="index"/>
        <label :for="'q'+index">
            {{ option.text }}
        </label>
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
input {
     margin-left: -1000px;
}

input:checked + label {
    background: #a7cf5f;
    background: #679436;
    color: #46660d;
}
</style>
