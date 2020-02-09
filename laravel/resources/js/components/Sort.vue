<template>
<div>
    <draggable tag="ol" @change="saveAnswer" :list="list">
            <li class="item" v-for="option in list" :key="option.name">
                {{ option.name }}
                {{ option.id }}
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
        list: function() {
            return this.question.choices.map((item, index) => {
                return { name: item.text, id: index }
            })
        },

        answer: function() {
            return JSON.stringify(this.list)
        }
    },

    methods: {
        saveAnswer() {
            let results = JSON.stringify(this.list.map(x => x.id))
            console.log(results)
            this.$emit('saved', results)
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
