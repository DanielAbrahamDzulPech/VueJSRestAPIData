<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Hello Vue 3 in CodeSandbox!" />
  <div>
    <!-- <li>{{ nombre }}</li> -->
    <input type="text" v-model="nombre" />
    <section class="section__first">
      <h1>Tu eres: {{ nombre }}</h1>
      <h2>Tu calle es: {{ dirección.calle }}</h2>
      <h3>Tu region es: {{ dirección.manzana }}</h3>
    </section>

    <section>
      <div>
        <div v-for="pokemon in info" :key="pokemon">
          <div class="card">
            <h4>{{ pokemon.name }}</h4>
            <h4>{{ pokemon.url }}</h4>
          </div>
        </div>

        <div v-for="pokemon in pokemones" :key="pokemon">
          <div class="card">
            <h1>aquii</h1>
            <h4>{{ pokemon.name }}</h4>
            <h4>{{ pokemon.url }}</h4>
          </div>
        </div>
      </div>
    </section>

    <div>
      {{ info }}
      {{ infoclima }}
      <h3>nombres</h3>
      <br />
      <!-- {{ info.name }} -->
    </div>
    <button @click="obtenerPokemones">Pokemones</button>
  </div>
</template>

<script>
import HelloWorldVue from "./components/HelloWorld.vue";
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      nombre: "Mayel Valencia",
      dirección: {
        calle: 123,
        manzana: 67,
        ruta: 4,
      },
      pokemones: [],
      info: null,
      //info: [],
      // no cierto era error del render - falto mapiar error con null
      infoclima: null,
      nombresss: {},
    };
  },
  components: {
    HelloWorld: HelloWorldVue,
  },
  mounted() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon/")
      .then((response) => (this.info = response.data.results));

    // axios
    //   .get("https://localhost:44374/WeatherForecast")
    //   .then((response) => (this.infoclima = response));
  },
  methods: {
    async obtenerPokemones() {
      try {
        // esperemos la respuesta de fetch y la guardamos en una constante | es lo mismo que esto  .then(res => res.json()) pero colocada una respuesta await
        // esperemos esta peticion y una vez esa peticion devuelva algo va a estar en este res
        const res = await fetch("https://pokeapi.co/api/v2/pokemon/");
        // nuestra const data va a esperar a res .json
        const data = await res.json();
        // resultado el mismo que fetch
        console.log(data.results);
        // this.pokemones = data;

        data.results.forEach((element) => {
          // console.log(element);
          console.log(element.name);
          this.pokemones = element;
        });

        // const arrayNombres = data.results.map(poke => poke.name);
        // const arrayNombres = data.results.filter(poke => poke.name === 'bulbasaur');

        // console.log(arrayNombres);
      } catch (error) {
        // podemos mostrar en console el error
        console.log(error);
      }
    },
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.section__first {
  padding: 10px;
  width: 250px;
  color: white;
  background-color: cadetblue;
  border-radius: 15px;
  margin-top: 15px;
  margin-bottom: 15px;
  margin-left: auto;
  margin-right: auto;
}

.card {
  background-color: magenta;
  color: white;
  padding: 20px 10px;
  border-radius: 5px;
  margin: 10px auto;
  width: 450px;
  /* max-width: 350px; */
}
</style>
