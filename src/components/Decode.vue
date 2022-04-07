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
            <span v-if="showPoem"> 
                Eight tall twins of steel and stone <br>
                The earthquake almost made them prone. <br>
                All of them sit near a fast pool <br>
                Two of them look at a school. <br>
                All of this is really true <br>
                But just the oldest hides a clue. <br>
                Look for it in it's buttcrack <br>
                A better description i do lack. <br>
                Worry not for sanitation <br>
                You will find a fresh sensation <br>
                (Iako pazimo na staklo)
            </span>
            <img  v-if="showImage" src="slikica.jpg" height="900px">
            <span v-if="showWordlish" >
                <br>
                budes valjda skuzila kak ovo ide :P <br> 
                <Guess solve="fish" class="wordl"></Guess>
                <Guess solve="cross" class="wordl"></Guess>
                <Guess solve="faith" class="wordl"></Guess>
                <Guess solve="plaque" class="wordl"></Guess>
                <Guess solve="inscription" class="wordl"></Guess>
                <Guess solve="code" class="wordl"></Guess>
                <Guess solve="volim te" class="wordl"></Guess>
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
        },

        showPoem: function (){
            if (this.guess == this.solution4){
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

.wordl{
    display: inline-block;
    padding: 10px;
}

</style>
