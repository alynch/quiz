<template>
    <div>
        <template v-for="(part, i) in prompt">
            <span v-if="part.type == 'blank'"><input @change="saveAnswer" class="input" :name="'q'+part.number" v-model="answers[part.number]"></span>
            <span v-else>{{ part.text }}</span>
        </template>
    </div>
</template>

<script>

export default {
    props: ['question'],

    data: function() {
        return {
            answers: (this.question.savedAnswer) ? JSON.parse(this.question.savedAnswer) : []
        }
    },

    computed: {
        prompt: function() {
            let regex = /(\[\d*\])/
            let parts = this.question.text.split(regex)

            let n = 0
            return parts.map(part => {
                let item = {}
                item.type = regex.test(part) ? 'blank' : 'text'
                item.text = part
                item.number = item.type == 'blank' ? n++ : null
                return item
            })
        },

        answer: function() {
            return JSON.stringify(this.answers)
        }
    },

    watch: {
        question: function () {
            console.log('watched input')
            this.answers = JSON.parse(this.question.savedAnswer) || []
        }
    },

    methods: {
        saveAnswer() {
            this.$emit('saved', this.answer)
	}
    }
}
</script>


<style>

div {
    line-height: 1.8;
}

.input {
    border: 1px solid #ccc;
    color: #666;
    max-width: 6em;
    border-radius: 5px;
    background: #f4f4f4;
    line-height: 1.4;
}

.input:focus {
    background: #bae1bd;
}
/*

label {
    display: block;
    width: 100%;
    padding: 5px;
    border: 1px solid #ccc;
    cursor: pointer;
}

label:hover {
    background: #ccc;
}

input {
     margin-left: -1000px;
}

input:checked {
    argin-left: 0;
}

input:checked + label {
    background: green;
    color: #eee;
}

*/
</style>
