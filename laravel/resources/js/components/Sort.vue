<template>
<div>
    <draggable @change="saveAnswer" v-model="answers">
        <ol v-for="(option, index) in answers" :key="option">
            <li class="item">
                {{ option }}
            </li>
        </ol>
    </draggable>
</div>
</template>

<script>

import draggable from 'vuedraggable'

export default {
    components: {
        draggable
    },

    props: ['question'],

    data: function() {
        return {
            answers: this.question.options
        }
    },

    computed: {
        answer: function() {
            return JSON.stringify(this.answers)
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

.item  {
    display: block;
    padding: 5px;
    border-radius: 5px;
    background: #f4f4f4;
    margin: 1em 0;
    cursor: pointer;
}
</style>
