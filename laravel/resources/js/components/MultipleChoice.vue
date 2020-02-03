<template>
<div>
    <div v-for="(option, index) in question.options">
        <input @change="saveAnswer" type="radio" :id="'q'+index" v-model="answer" name="q" :value="index"/>
        <label :for="'q'+index">
            {{ option }}
        </label>
    </div>
</div>
</template>

<script>

export default {
    props: ['question'],

    data: function() {
        return {
            answer: null
        }
    },

    methods: {
        saveAnswer() {
            localStorage.setItem('q.' + this.question.id, this.answer);
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
