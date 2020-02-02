<template>
<div>
    <div v-for="(option, index) in options">
        <input type="radio" :id="'q'+index" v-model="answer" name="q" :value="index"/>
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
            answer: null
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
    color: #46660d;
}
</style>
