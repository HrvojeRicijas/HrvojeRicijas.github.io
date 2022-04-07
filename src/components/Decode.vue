<template>
    <div>
        <div>
            <span>Please enter the code in the right order:    </span>
            <input class="input" type="text" v-model="guess">
        </div>
        <div class="output">
            <span v-if="showPolice"> 
                Postoji jedna stara prica, koja se prica jos od davnog utorka.
                Bio jednom jeda policajac u gornjoj kustosiji.
                Bio je to najhrabriji policajac kojeg je gornja kustosija ikada vidjela.
                Držao je cestu prema stanici sigurnom svakoga dana svakoga tjedna, da djeca obliznje skole ne moraju brinuti.
                No taj policajac imao je tajnu koju je cuvao svim silama.
                Kako su dani prolazili, policajac je bio stariji i stariji, pa stariji jos.
                Došao je onda, konacan dan, no policajac nije htio odustati od svojega posla.
                Odlucio je cak i u smrti cuvati djecu obliznje skole.
                Sada, i dan danas, u svojem grobu, on pazi na cesti prema stanici, čuva djecu i svoju tajnu.
                (djeca nisu u grobu)
                </span>
            <img  v-if="showImage" src="slikica.jpg" height="900px">
            <span v-if="showWordlish" > 
                <Guess solve="fish" style="float:center; padding:25px"></Guess>
                <Guess solve="cross" style="float:center; padding:25px"></Guess>
                <Guess solve="faith" style="float:center; padding:25px"></Guess>
                <Guess solve="plaque" style="float:center; padding:25px"></Guess>
                <Guess solve="inscription" style="float:center; padding:25px"></Guess>
                <Guess solve="code" style="float:center; padding:25px"></Guess>
            </span>
        </div>
    </div>
</template>

<script>

import Guess from './Guess.vue'

export default {
    name: 'Code',
    components: {
        Guess,
    },

    props: {},
    data: function (){
        return {
            guess: "",
            solution: "39867",
            solution2: "0504",
            solution3: "inri",
            solution4: "poem"
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
        showImage: function (){
            if (this.guess.toLowerCase() == this.solution3){
               return 1;
            }
            return 0;
        },

        showWordlish: function (){
            if (this.guess == this.solution2){
               return 1;
            }
            return 0;
        },

        showPolice: function (){
            if (this.guess == this.solution){
               return 1;
            }
            return 0;
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
