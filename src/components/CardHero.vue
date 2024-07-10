<template>
  <div class="card-hero">
    <p>Nombre {{ hero.name }}</p>
    <img>
    <p>Poder</p>
    <p>Raza</p>
    <p>Publicado por:</p>
    <button @click="eliminarHero">X</button>
  </div>
</template>

<script>
export default {
  name: "CardHero",
  props: {
    hero: Object
  },
  methods: {
    eliminarHero() {
      this.$emit("eliminar", this.hero);
    }
  }
};


</script>

<style>
.card-hero{
border: 5px groove black;
border-radius: 8px;
padding: 1rem;
width: 200px;
height: 300px;
overflow: hidden;
}
</style>
