<template>
<div>
    <div v-for="(option, index) in question.choices">
        <input @change="saveAnswer" type="checkbox" :id="'q'+index" :name="'q'+index" v-model="answers" :value="index"/>
        <label :for="'q'+index">
            {{ option.text }}
        </label>
    </div>
</div>
</template>

<script>

export default {
    props: ['question'],
    data: function() {
        return {
            answers: JSON.parse(this.question.savedAnswer) || []
        }
    },

    watch: {
        question: function () {
            this.answers = JSON.parse(this.question.savedAnswer) || []
        }
    },

    computed: {
        answer: function() {
            return JSON.stringify(this.answers.sort())
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

label {
    position: relative;
}

input:checked + label::after {
    content: '✓';
    position: absolute;
    right: 10px;
    top: 2px;
    color: #46660d;
    font-size: 1.6em;
    font-weight: bold;
}
</style>
