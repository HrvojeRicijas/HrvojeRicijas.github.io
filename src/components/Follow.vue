<template>
  <div v-on:mouseover="mousePos($event)" class="object">
      <span class="thing" :style="style" > Hello </span>
  </div>
</template>

<script>
export default {
    name: 'Follow',

    props:{

    },

    data: function (){
        return {
            position: {
                x: 300,
                y: 0,
            },



        }

    },

    methods:{

        mousePos: function()
        {
            console.log(event);
            this.position['y'] = event.clientY;
            this.position['x'] = event.clientX;
        }
    },

    computed:{
        style(){
            return 'top: ' + this.position['y'] + 'px; left: ' + this.position['x'] + 'px'
        }
    },

}
</script>

<style>
.object{

    display: inline-flex;

}

.thing{
    border: 0.25rem;
    border-radius: 1rem;
    background-color: rgb(170, 0, 0);
    color: rgb(255, 200, 0);
    border-style: solid;
    padding: 2rem;
    font-size: 2rem;
    position: absolute;
    height: 5rem;
    width: 5rem;
    text-align: center;
    vertical-align: middle;
}
</style>
