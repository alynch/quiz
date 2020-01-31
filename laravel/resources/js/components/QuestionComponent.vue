<template>
		<div style="position:relative" class="p-6 bg-white rounded-lg shadow-xl">
                <div class="question-number">
                    {{ id }} / {{ total }}
                </div>

				<h4 class="text-lg text-gray-900 mb-6">
					{{ question.title }}
				</h4>
				<p class="text-gray-800">
					{{ question.prompt }}
				</p>

                
                <div v-for="(option, index) in question.options"
                    class="text-gray-700 mt-2">
                        <input :type="question.type" :id="index" :name="'q' + id" :value="id"/>
                    <label :for="index">
                        {{ option }}
                    </label>
                </div>
		</div>
    </div>
</template>

<script>

export default {
    props: ['id', 'total', 'question'],

 	data: function() {
		return {
			currentView: null
		}
	},

	mounted() {
            console.log('Component mounted.')
        }
    }

</script>


<style>
.question-number {
	background: #ffffff;
	color: #6a6a6a;
	border: 1px solid #dedede;
	border-radius: 5px;
	box-shadow: 0 1px 3px rgba(0, 0, 0, 0.25);
	padding: 5px;
	position: absolute;
	top: 2em;
	right: -3em;
	width: 4em;
	margin-left: 1em;
	text-align: center;
}

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


</style>
