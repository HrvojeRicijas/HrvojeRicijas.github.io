<template>

    <div style="display: inline;"
        v-on:keydown.up="clicked(2)"
        v-on:keydown.left="clicked(1)"
        v-on:keydown.right="clicked(3)"
        v-on:keydown.down="clicked(4)"
    >
        <div style="display:flex">
            <button class="but" v-on:click="clicked(1)">◄</button>
        </div>
        <div style="display:block">
            <button class="but" v-on:click="clicked(2)">▲</button>
            <br>
            <button class="but" v-on:click="clicked(4)">▼</button>
        </div>
        <div style="display:flex">
            <button class="but" v-on:click="clicked(3)">►</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Movepad',

    props:{

    },

    data: function (){
        return {

        }

    },

    methods:{
        clicked (side){
            this.$emit ('move', side)
        }

    },

    computed:{

    },


}
</script>

<style>

.but{
    height: 7rem;
    width: 7rem;
    font-size: 3rem;
    margin: auto ;

}


</style>
