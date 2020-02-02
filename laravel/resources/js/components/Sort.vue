<template>
<div>
    <draggable v-model="answers">
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

    props: ['options'],

    data: function() {
        return {
            answers: this.options
        }
    },

    computed: {
        answer: function() {
            return JSON.stringify(this.answers)
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
