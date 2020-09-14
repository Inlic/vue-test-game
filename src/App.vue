<template>
  <div id="app" class="container-fluid">
    <div class="row">
      <div class="card col-3" v-for="planet in planets" :key="planet.name">
        <img class="img-fluid" :src="planet.imgUrl"/>
        <div class="card-body">
          <h4 class="card-title"> {{ planet.name }}</h4>
          <p class="card-text">Vespene Gas: {{planet.vespeneGas}}</p>
          <p class="card-text">Pylons: {{planet.pylons}}</p>
          <p class="card-text" v-if="planet.demons >= 0">Demons: {{planet.demons}} </p>
          <p class="card-text" v-if="planet.hunger >= 0">Hunger: {{planet.hunger}} </p>
          <button class="btn btn-success" @click="mineVespene(planet)">Mine Vespene</button>
          <button class="btn btn-primary" @click="giveVespene(planet)">Give Vespene</button>
        </div>
      </div>
      <div class="row">
        <div class="col-12"><h4>Banked Vespene: {{bankedVespene}}</h4>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  mounted(){
    setInterval(()=> {
      this.demonsUp()
    }, 5000);
    setInterval(()=> {
      this.hungerUp()
    }, 8000);
    setInterval(()=> {
      this.generateVespene()
    }, 2000);
  },
  data(){
    return {
      bankedVespene: 0,
      planets: [
        {
          name: "Venus",
          vespeneGas: 0,
          pylons: 0,
          imgUrl: "https://scitechdaily.com/images/Venus-Planet.jpg"
        },
        {
          name: "Mars",
          vespeneGas: 0,
          pylons: 0,
          demons: 0,
          imgUrl: "https://solarsystem.nasa.gov/internal_resources/3841"
        },
        {
          name: "Jupiter",
          vespeneGas: 0,
          pylons: 0,
          hunger: 0,
          imgUrl: "https://cdn.mos.cms.futurecdn.net/iEv6pmS4gfbefs5JbwHWiJ.png"
        },
        {
          name: "Saturn",
          vespeneGas: 0,
          pylons: 0,
          demons: 0,
          hunger: 0,
          imgUrl: "https://upload.wikimedia.org/wikipedia/commons/c/c7/Saturn_during_Equinox.jpg"
        }
      ]
    }
  },
  methods: {
    generateVespene(){
      for(let key in this.planets){
        let planet = this.planets[key]
        if(planet.name == "Venus"){
          planet.vespeneGas+=4
        }
      }
    },
    giveVespene(target){
        if(this.bankedVespene > 0){
          target.vespeneGas+=1
          this.bankedVespene-=1
        }
      },
    mineVespene(target){
        if(target.vespeneGas > 0){
          target.vespeneGas-=1
          this.bankedVespene+=1
        }
      },
    demonsUp(){
      for(let key in this.planets){
        let planet = this.planets[key]
        if(planet.demons >=0){
        planet.demons+=5
        }
      }
    },
    hungerUp(){
      for(let key in this.planets){
        let planet = this.planets[key]
        if(planet.hunger >= 0){
        planet.hunger+=10
        }
      }
    }
  }
}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
