<template>
    <div>
        <div>
            <input v-if="inputCondition" class="input" type="text" v-model="guess">
        </div>
        <div class="output">
            <span v-for="(letter, key) in guess" :key="key" :style="letterColor(key)">{{letter}}</span>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Guess',
    props: {},
    data: function (){
        return {
            guess: "",
            solution: "Dorotea je najzgodnija cura na svijetu",
        }
    },

    methods:{
        letterColor: function(key){
            if (this.guess.toLowerCase() == this.solution.toLowerCase()) {
                return {
                    color: "#0000e6",
                    fontSize: "1rem",
                }
            }
            if (this.guess[key].toLowerCase() == this.solution[key].toLowerCase()) {
                return {
                    color: "#39e600",
                    fontSize: "1rem",
                }
            }

            return {
                color: "#ff0d0d",
                fontSize: "1rem",
            };
        }
    },

    computed:{
        inputCondition: function (){
            if (this.guess){
                return this.guess.toLowerCase() != this.solution.toLowerCase()
            }
            return 1;
        }

    }
}
</script>

<style scoped>

.output{
    font-size: 1rem;
}

.input{
    min-width: 10rem;
    min-height: 1rem;
    font-size: 1rem;
    border-radius: 1rem;
    padding: 0.25rem
}

</style>
