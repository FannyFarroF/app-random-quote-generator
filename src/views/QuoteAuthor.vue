<template>
  <div class="QuoteAuthor py-3">
    <div class="container">
      <div class="d-flex justify-content-between">
        <router-link to="/" class="btn d-flex">
          <span class="material-icons-outlined">
            home
          </span>
        </router-link>

        <ButtonComponent v-on:random="ejecutarRandom($event)" />
      </div>

      <h1>{{ authorPerfil }}</h1>

      <ul class="p-0">
        <li v-for="(item, index) in datos" :key="index" class="my-2">
          <div class="quotes ">
            <div class="box-quotes">
              <p class="my-0  text-start">"{{ item.quoteText }}"</p>
            </div>
          </div>
        </li>
      </ul>
      <CreditsComponent />
    </div>
  </div>
</template>
<script>
  import axios from "axios";
  import ButtonComponent from "@/components/ButtonRandomComponent.vue";
  import CreditsComponent from "@/components/CreditsComponent.vue";

  export default {
    data() {
      return {
        datos: [],
        authorPerfil: "",
      };
    },
    components: {
      ButtonComponent,
      CreditsComponent,
    },
    mounted() {
      this.cargarDatos();
    },
    methods: {
      cargarDatos() {
        const author = location.pathname.replace("/quoteAuthor/", "");
        axios
          .get(
            `https://quote-garden.herokuapp.com/api/v3/quotes/random?author=${author}&count=4`
          )
          .then((response) => {
            let data = response.data;
            this.datos = data.data;
            this.authorPerfil = data.data[0].quoteAuthor;
          })
          .catch((error) => console.log("Error", error));
      },
      ejecutarRandom(value) {
        if (value) {
          this.cargarDatos();
        }
      },
    },
  };
</script>
<style lang="scss" scoped>
  a {
    border: 1px solid #eee !important;

    &:hover {
      background: #eee;
    }
  }
  ul li {
    list-style: none;
  }
  h1 {
    font-style: normal;
    font-weight: bold;
    font-size: 36px;
    line-height: 42px;

    color: #333333;
  }
</style>
