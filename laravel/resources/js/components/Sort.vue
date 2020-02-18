<template>
<div>
    <draggable tag="ol" @change="saveAnswer" :list="list">
            <li class="item" v-for="option in list" :key="option.id">
                {{ option.name }}
            </li>
        </ol>
    </draggable>

    <div v-if="review">
        Score: {{ score }}
    </div>

</div>
</template>

<script>

import draggable from 'vuedraggable'

export default {
    components: {
        draggable
    },

    props: ['review', 'question'],

    data: function() {
        return {
            answers: this.question.choices,
            list: []
        }
    },

    computed: {
        answer: function() {
            return JSON.stringify(this.answers)
        },

        score: function() {
            if (!this.question.savedAnswer) {
                return 0;
            }

            let a = JSON.stringify(this.list.map(x => x.id))
            let b = this.question.savedAnswer
            console.log('A:' + a)
            console.log('B: '+ b)

            if (a === b) {
                return 1
            } else {
                return 0
            }
        }
    },

    methods: {
        saveAnswer() {
            let results = JSON.stringify(this.list.map(x => x.id))
            this.$emit('saved', results)
	}
    },

    created() {

        this.list = this.question.choices.map((item, index) => {
                return { name: item.text, id: index }
            })

            // if we have a saved answer, sort values according to it
            if (this.question.savedAnswer) {
                let sortArray = JSON.parse(this.question.savedAnswer)
                
                this.list.sort(function(a, b){
                    return sortArray.indexOf(a.id) - sortArray.indexOf(b.id);
                });
            }
    },

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
