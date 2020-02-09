<template>
<div>
    <div v-for="(option, index) in question.choices">
        <input @change="saveAnswer" type="radio" :id="'q'+index" v-model="answer" name="q" :value="index"/>
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
            answer: this.question.savedAnswer
        }
    },

    watch: {
        question: function () {
            this.answer = this.question.savedAnswer
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
