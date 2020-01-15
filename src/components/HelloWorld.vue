<template>
  <div>
    <div class="hello">
      Welcome to the Candy Store
    </div>
    <div class="store">

      <div class="materials">
        <div style="display:inline-flex">
          <div style="padding:1rem">
            <div v-for="(stat , material) in materials" :key="material" style="display:block">
              <span class="clickable" v-on:click=" (parts['material'] = material); buildIcecream(); parts['mw'] = materials[parts['material']]['mw'][0]" >{{material.replace("_", " ")}}</span>
            </div>
          </div>

          <div v-if="parts['material']" style=" background-color:rgb(245, 187, 187); padding:1rem;">
            <div style="display:block" v-for="mw in materials[parts['material']]['mw']" :key="mw">
              <span class="clickable" v-on:click="parts['mw'] = mw; buildIcecream()"> Mw {{mw}}</span>
            </div>
          </div>
        </div>
      </div>

      <div class="weapons">
        <div v-for="(stat , weapon) in weapons" :key="weapon">
          <span class="clickable" v-on:click=" (parts['weapon'] = weapon); buildIcecream()">{{weapon.replace("_", " ")}}</span>
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
        material: "",
        mw: 1,
        weapon: "",
        container: "",
      },

      materials: {
        Iron: {
          cost: 1,
          hardness: 5,
          mw: [1, 2, 3],
          hp: 3,
          special: ""
        },
        Copper: {
          cost: 1,
          hardness: 4,
          mw: [1, 2, 3],
          hp: 3,
          special: "Doesn't rust"
        },
        Steel: {
          cost: 3,
          hardness: 7,
          mw: [2, 3, 4],
          hp: 3,
          special: ""
        },
        Silver: {
          cost: 5,
          hardness: 4,
          mw: [2, 3, 4],
          hp: 3,
          special: ""
        },
        Tempered_glass: {
          cost: 5,
          hardness: 8,
          mw: [2, 3, 4],
          hp: 2,
          special: "Additional slashing damage"
        },
        White_steel: {
          cost: 8,
          hardness: 9,
          mw: [3, 4, 5],
          hp: 3,
          special: "Weighs less"
        },
        Black_steel: {
          cost: 8,
          hardness: 9,
          mw: [3, 4, 5],
          hp: 3,
          special: "Heavier and more damaging"
        },
      },

      weapons: {
        Small: {
          cost: 2,
          damage: 6,
          type: "sl",
        },
        Medium: {
          cost: 2.5,
          damage: 8,
          type: "sl",
        },
        Large: {
          cost: 3,
          damage: 10,
          type: "sl",
        },
        Two_handed: {
          cost: 3.5,
          damage: 12,
          type: "sl",
        },
        Special: {
          cost: 4,
          damage: 6+6+6,
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
      var out = "";
      var material = this.parts["material"].replace('_', ' ').toLowerCase();
      var weapon = this.parts["weapon"].replace('_', ' ').toLowerCase();
      // var cn = this.parts["container"].replace('_', ' ').toLowerCase( );
      var mw = this.parts["mw"];
      if (material){out = out + "Masterwork " + mw + " " + material + " " + weapon + " weapon"}
    
      this.icecream = out;
    },
  },
  computed:{
    price: function(){
      if ((this.parts['material']+this.parts['weapon']+this.parts['container'])){
        return 1 *
        (this.parts['material'] ? this.materials[this.parts["material"]]["cost"] : 1) *
        (this.parts['mw'] ? 2**(this.parts['mw']-1) : 1) *
        (this.parts['weapon'] ? this.weapons[this.parts["weapon"]]["cost"] : 1) *
        (this.parts['container'] ? this.containers[this.parts["container"]]["cost"] : 1);
      }
      return 0;
    },
    taste: function(){
      if ((this.parts['material']+this.parts['weapon']+this.parts['container'])){
        return 1 *
        (this.parts['material'] ? this.materials[this.parts["material"]]["hardness"] : 1) *
        (this.parts['weapon'] ? this.weapons[this.parts["weapon"]]["damage"] : 1) *
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
.materials{
  display:inline-block;
  margin: 1rem;
  text-align: left;
  background-color: rgb(255, 197, 197);
  /* padding: 1rem; */
  min-width: 7rem;
}
.weapons{
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
