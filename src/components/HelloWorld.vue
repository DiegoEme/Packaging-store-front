<template>
  <div>
    <v-toolbar color="blue">
      <v-toolbar-title class="d-flex">
        <router-link class="b login" to="/login">Login</router-link>
        <v-spacer class="spacer"></v-spacer>
        <li><a class="b" href="#servicios">Servicios</a></li>
        <li><a class="b" href="#nosotros">Nosotros</a></li>
      </v-toolbar-title>
    </v-toolbar>
    <article class="caja">
      <img
        src="https://www.enveleuropa.com/wp-content/uploads/2020/08/envel_banner-02_1200x390_b.jpg"
        alt=""
      />
    </article>

<div id="servicios">

    <v-container >
      <v-row class="d-flex justify-space-around mt-10">
        <v-card
          v-for="movie of movies"
          :key="movie"
          class="mx-10 mb-10"
          max-width="344"
        >
          <v-img :src="movie.codigo" height="200px"></v-img>

          <v-card-title>
            <a :href="movie.url"> {{ movie.nombre }}</a>
          </v-card-title>

          <v-card-text>
            {{ movie.descripcion }}
          </v-card-text>

          <v-card-actions>
            <v-btn color="orange lighten-2" text>
              Ver
            </v-btn>

            <v-spacer></v-spacer>

            <v-btn icon @click="show = !show">
              <v-icon>{{
                show ? "mdi-chevron-up" : "mdi-chevron-down"
              }}</v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-row>
    </v-container>
</div>
    <div id="nosotros">
      <v-container>
        <v-row>
          <p>
            Contamos con la capacidad, recursos y tecnologías adecuadas para
            llevar satisfacer sus necesidades.
          </p>
          <p>
            Transformamos con precisión sus ideas en empaques diseñados
            específicamente para su necesidad.
          </p>
          <p>
            Manejamos tres tipos de impresión: Screen, Impresiín UV y litografía
          </p>
        </v-row>
      </v-container>
    </div>

    <footer>
      <h5>© Todos los derechos reservados</h5>
    </footer>

    <!-- <div class="container mt-5">
      <div class="row">
        <div
          v-for="movie of movies"
          :key="movie"
          class="card col-5 border-dark"
          style="width: 18rem;"
        >
          <div class="caja">
            <img class="card-img-top" :src="movie.image" />
          </div>

          <div class="card-body">
            <h5 class="card-title">
              <a :href="movie.url"> {{ movie.title }}</a>
            </h5>
            <p class="card-text">{{ movie.description }}</p>
          </div>
        </div>
      </div>
    </div>  -->
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "NewsCard",
  data() {
    return {
      movies: null,
    };
  },
  mounted() {
    axios
      .get(
        "http://localhost:3000/api/articulo/list"

        // "https://gnews.io/api/v4/top-headlines?token=e6e3589416050f17d6f669dfcf8329ef&lang=es&max=4"
      )
      .then((response) => {
        console.log(response.data);
        this.movies = response.data;
        console.log(this.movies);
      });
  },
};
</script>

<style scoped>

div {
  scroll-behavior: smooth;
}
#servicios {
  background-image: url("https://www.pouadvocats.com/wp-content/uploads/2018/02/Light-Grey-Background-Texture-4.jpg");
}
.caja {
height: 350px;
width: 100vw;
}

.caja img {
height: 100%;
width: 100%;
object-fit: cover;
}

.b {
  color: blanchedalmond !important;
  text-decoration: none;
}

.login {
  margin: 0 20px;
}

.b:visited {
  text-decoration: none;
}
footer {
  background-color: black;
  color: white;
  height: 50px;
}
h5 {
  text-align: center;
  margin: auto;
  padding-top: 15px;
}

#nosotros {
  background-color: blanchedalmond;
}

p {
  text-align: center;
  margin: 20px 150px;
  font-size: 30px;
}
li {
  color: blanchedalmond !important;
  text-decoration: none;
  list-style-type: none;
  margin: 0 20px;
}

.card {
  margin: 10px auto;
}

.caja {
  height: 300px;
}

.card img {
  height: 100%;
  width: 100%;
  object-fit: cover;
}
</style>
