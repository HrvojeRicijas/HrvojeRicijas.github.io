<template>
  <div>
    <div class="hello">
      Welcome to the Candy Store
    </div>
    <div class="store">

      <div class="flavors">
        <div style="display:inline-flex">
          <div style="padding:1rem">
            <div v-for="(stat , flavor) in flavors" :key="flavor" style="display:block">
              <span class="clickable" v-on:click=" (parts['flavor'] = flavor); buildIcecream(); parts['mw'] = flavors[parts['flavor']]['mw'][0]" >{{flavor.replace("_", " ")}}</span>
            </div>
          </div>

          <div v-if="parts['flavor']" style=" background-color:rgb(245, 187, 187); padding:1rem;">
            <div style="display:block" v-for="mw in flavors[parts['flavor']]['mw']" :key="mw">
              <span class="clickable" v-on:click="parts['mw'] = mw; buildIcecream()"> Mw {{mw}}</span>
            </div>
          </div>
        </div>
      </div>

      <div class="toppings">
        <div v-for="(stat , topping) in toppings" :key="topping">
          <span class="clickable" v-on:click=" (parts['topping'] = topping); buildIcecream()">{{topping.replace("_", " ")}}</span>
        </div>
      </div>

      <div class="containers">
        <div v-for="(stat , container) in containers" :key="container">
          <span class="clickable" v-on:click=" (parts['container'] = container); buildIcecream()">{{container.replace("_", " ")}}</span>
        </div>
      </div>

    </div>

    <div class="icecream">
      <label>{{icecream}}</label>
    </div>

    <div class="price">
      <div>For which you have to pay</div>
      <div class="number">{{price}}$</div>
    </div>

    <div class="taste">
      <div>Experts rate it a solid </div>
      <div class="number" :style="bgc">{{taste.toFixed(2) }}/10</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data: function () {
    return {
      icecream: "You have nothing",

      parts: {
        flavor: "",
        mw: 1,
        topping: "",
        container: "",
      },

      flavors: {
        Chocolate: {
          cost: 1,
          taste: 5,
          mw: [1, 2, 3],
          hp: 3,
          special: ""
        },
        Vanilla: {
          cost: 1,
          taste: 4,
          mw: [1, 2, 3],
          hp: 3,
          special: "Doesn't rust"
        },
        Strawberry: {
          cost: 3,
          taste: 7,
          mw: [2, 3, 4],
          hp: 3,
          special: ""
        },
        Lemon: {
          cost: 5,
          taste: 4,
          mw: [2, 3, 4],
          hp: 3,
          special: ""
        },
        Cherry: {
          cost: 5,
          taste: 8,
          mw: [2, 3, 4],
          hp: 2,
          special: "Additional slashing damage"
        },
        White_chocolate: {
          cost: 8,
          taste: 9,
          mw: [3, 4, 5],
          hp: 3,
          special: "Weighs less"
        },
        Black_chocolate: {
          cost: 8,
          taste: 9,
          mw: [3, 4, 5],
          hp: 3,
          special: "Heavier and more damaging"
        },
      },

      toppings: {
        Sprinkles: {
          cost: 2,
          taste: 6,
          type: "sl",
        },
        Cookie_crumbs: {
          cost: 2.5,
          taste: 8,
          type: "sl",
        },
        Caramel: {
          cost: 3,
          taste: 10,
          type: "sl",
        },
        Cheese: {
          cost: 3.5,
          taste: 12,
          type: "sl",
        },
        Skittles: {
          cost: 4,
          taste: 6+6+6,
          type: "sl",
        },
      },

      containers: {
        Paper_cup : {
          cost: 1,
          taste: 1
        },
        Cone: {
          cost: 2,
          taste: 1.1
        },
        Glass_bowl: {
          cost: 3,
          taste: 1.3
        },
        Chocolate_cone: {
          cost: 2.5,
          taste: 1.7
        },
      }
    }
  },
  methods:{
    buildIcecream: function () {
      var out = "You have ";
      var fl = this.parts["flavor"].replace('_', ' ').toLowerCase();
      var tp = this.parts["topping"].replace('_', ' ').toLowerCase();
      var cn = this.parts["container"].replace('_', ' ').toLowerCase();
      if (fl){out = out + "a lovely scoop of " + fl + " ice cream"}
      if (tp){out = out + (fl ? ", covered with " : "") + tp}
      if (cn){out = out + (tp+fl ? ", in " : " ") + "a nice " + cn} else if (fl || tp) {out = out + ", melting in your hands"}
      this.icecream = out;
    },
  },
  computed:{
    price: function(){
      if ((this.parts['flavor']+this.parts['topping']+this.parts['container'])){
        return 1 *
        (this.parts['flavor'] ? this.flavors[this.parts["flavor"]]["cost"] : 1) *
        (this.parts['mw'] ? 2**(this.parts['mw']-1) : 1) *
        (this.parts['topping'] ? this.toppings[this.parts["topping"]]["cost"] : 1) *
        (this.parts['container'] ? this.containers[this.parts["container"]]["cost"] : 1);
      }
      return 0;
    },
    taste: function(){
      if (this.parts['topping']=="Cheese" && this.parts['flavor'] == ""){
        if (this.parts['container'] == "Paper_cup") {return 9}
        if (this.parts['container'] == "Glass_bowl") {return 10}
      }
      if ((this.parts['flavor']+this.parts['topping']+this.parts['container'])){
        return 1 *
        (this.parts['flavor'] ? this.flavors[this.parts["flavor"]]["taste"] : 1) *
        (this.parts['topping'] ? this.toppings[this.parts["topping"]]["taste"] : 1) *
        (this.parts['container'] ? this.containers[this.parts["container"]]["taste"] : 1);
      }
      return 0;
    },
    bgc: function(){
      return "background-color: rgb(" + (255 - (this.taste*25)) + ", " + (this.taste*25) + ", 0)"
    }

  },
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}

.clickable{
  display: flex;
  padding: 0.2rem;
}

.clickable:hover{
  background-color: rgb(0, 0, 0, 0.1);
}

.hello{
  font-size: 4rem;
  color:rgb(255, 101, 126);
}

.store{
  display: inline-flex;
  flex-direction: row;
  align-items: center;
  /* background-color:rgb(187, 110, 10); */

}
.flavors{
  display:inline-block;
  margin: 1rem;
  text-align: left;
  background-color: rgb(255, 197, 197);
  /* padding: 1rem; */
  min-width: 7rem;
}
.toppings{
  display: inline-block;
  margin: 1rem;
  text-align: center;
  background-color: rgb(209, 255, 197);
  padding: 1rem;
  min-width: 7rem;
}
.containers{
  display: inline-block;
  margin: 1rem;
  text-align: right;
  background-color: rgb(197, 246, 255);
  padding: 1rem;
  min-width: 7rem;
}

.icecream{
  margin-top: 1rem;
  margin-bottom: 1rem;
  font-size: 2rem;
}

.price{
  font-size: 1rem;
  margin:1rem;
}

.number{
  background-color: #42b983;
  border-radius: 50%;
  border-style: solid;
  border-width: 3px;
  color: rgb(255, 255, 255);
  font-size: 3rem;
  display: inline-block;
  margin: auto;
  margin-top: 1rem;
  margin-bottom: 1rem;
  padding: 1rem;


}

</style>

// metal
//   cost
//   dr
//   mw
//   hp
//   special
// wep
//   cost
//   dmg
//   weight
//   type
