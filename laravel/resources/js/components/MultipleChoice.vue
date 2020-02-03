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
    props: ['id', 'question'],

    data: function() {
        return {
            answer: null
        }
    },

    methods: {
        saveAnswer() {
            console.log(this.answer)
            localStorage.setItem('q.' + this.id, this.answer);
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
