<script>
// import { RouterLink, RouterView } from "vue-router";

import { morthyApi } from "@/api/morthyApi";

export default {
  name: "App",

  data() {
    return {
      personajeData: {},
      personajeID: "",
    };
  },

  methods: {
    async searchPersonaje() {
      try {
        const personajeToFind = await fetch(`${morthyApi}/${this.personajeID}`)
          .then((response) => response.json());
        const personaje = personajeToFind;
        this.personajeData = personaje;
        console.log(personaje);
        return personaje;
      } catch (error) {
        alert("personaje was not found");
      }
    },
  },
};
</script>

<template>
  <header>
    <label for="">
      tipo de personaje por id:
      <input type="text" v-model="personajeID" />
      <button class="searchBtn" @click="searchPersonaje">Search personaje</button>
    </label>
  </header>

  <main v-if="Object.entries(personajeData).length > 0">
     <!-- si el personaje data tiene contenido -->
    <section class="personajeCard">
      <div class="nameImg">
        <h1 class="personajeName">{{ personajeData.name }}</h1>
        <img :src="personajeData.image" :alt="personajeData.name" />
      </div>

      <ul class="date">
        <h2>Date</h2>
        <li>
          <span >name: {{ personajeData.name }}</span>
        </li>
        <li>
          <span >status: {{ personajeData.status }}</span>
        </li>
        <li>
          <span >species: {{ personajeData.species }}</span>
        </li>
        <li>
          <span >gender: {{ personajeData.gender }}</span>
        </li>
        <li>
          <span > origin: {{ personajeData.origin.name }}</span>
        </li>
      </ul>

    </section>
  </main>
</template>

<style scoped lang="scss">
@import './personaje_types.scss';
@import url('https://fonts.googleapis.com/css2?family=Changa:wght@400;700&display=swap');

header{
  font-size: 30px;
  margin: 10px;
  height: auto;
  width: 600px;
}
label{
  display: flex;
  justify-content: center;
}
h1, h2{
  text-align: center;
  font-weight: 700;
}
main{
  display: flex;
  flex-direction: column;
  align-items: center;
}
.personajeCard{
  border-radius: 19px;
  background: rgba(6, 90, 49, 0.461);
  padding: 30px;
}
.nameImg {
  display: flex;
  flex-direction: column;
  align-items: center;
}
img{
  border-radius: 10px;
}
input{
  height: 40px;
  width: 55px;
  text-align: center;
  margin: 0;
  margin-left: 40px;
}

.searchBtn {
  height: 40px;
  width: 100px;
  font-weight: 600;
}
.date{
  list-style: none;
  line-height: 3;
}
.date li{
  font-size: 18px;
}

</style>
