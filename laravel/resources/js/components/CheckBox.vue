<template>
<div>
    <div v-for="(option, index) in options">
        <input type="checkbox" :id="'q'+index" :name="'q'+index" v-model="answers" :value="index"/>
        <label :for="'q'+index">
            {{ option }}
        </label>
    </div>
</div>
</template>

<script>

export default {
    props: ['options'],
    data: function() {
        return {
            answers: []
        }
    },

    computed: {
        answer: function() {
            return JSON.stringify(this.answers.sort())
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
