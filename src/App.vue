<template>
  <div>
    <div>
      <label>Encuentra tu Super Hero</label>
      <input id="superHero" type="number" v-model="idHero" required>
    </div>
    <div>
      <button @click="setSuperHero" :disabled="heros.length > 9">Cargar Super Hero</button>
      <!--ul>
        <li v-for="(superHero, index) in heros" :key="index">
          {{ superHero.name }} - {{ superHero.powerstats.power }} - {{ superHero.appearance.race }} - {{ superHero.placeofbirth.publisher }}
        </li>
      </ul-->
    </div>
    <section>
      <CardHero
        v-for="(hero, index) in heros"
        :key="index"
        :hero="hero"
        @eliminar="eliminarHero(index)" />
    </section>
  </div>
</template>

<script>
import CardHero from './components/CardHero.vue';
import axios from "axios";


export default {
  name: 'App',
  components: {
    CardHero
  },
  data() {
    return {
      idHero: "",
      heros: [], // Inicializado como arreglo vacío
      name: "",
      power: "",

    };
  },
  methods: {
    async getHero(url) {
      try {
        const { data } = await axios.get(url);
        console.log(data);
        return data;
      } catch (error) {
        console.log(error);
      }
    },

    async setSuperHero() {
      const url = `https://superheroapi.com/api.php/3033707663582647/${this.idHero}`;
      console.log(url);
      const HeroResponse = await this.getHero(url); //Espera respueta de getHero
      console.log(HeroResponse);
      // Verifica si HeroResponse es un objeto y lo convierte en un arreglo
      if (HeroResponse) {
        this.heros.push(HeroResponse);
      }
    },

    eliminarHero(index) {
      this.heros.splice(index, 1)
    }
  },


};
</script>

<style>
section {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  width: 80%;
  margin-top: 2rem;
}
</style>
