<template>
  <div class="home">
    <div class="spinner" v-show="hayDatos == false">
      <div class="spinner-grow text-info"></div>
    </div>
    <div class="container" v-show="hayDatos == true">
      <div class="content-home py-3">
        <div class="d-flex justify-content-end">
          <ButtonComponent v-on:random="ejecutarRandom($event)" />
        </div>
        <div class="quotes ">
          <div class="box-quotes">
            <p class="my-0  text-start">"{{ datos.quoteText }}"</p>
          </div>
          <div class="box-author-quotes py-3">
            <router-link
              :to="'/quoteAuthor/' + datos.quoteAuthor"
              class="enlace"
            >
              <p class="my-0  text-start">{{ datos.quoteAuthor }}</p>
              <p class="my-0  text-start type">{{ datos.quoteGenre }}</p>
            </router-link>
          </div>
        </div>
      </div>
      <CreditsComponent />
    </div>
  </div>
</template>

<script>
  import axios from "axios";

  // @ is an alias to /src
  import ButtonComponent from "@/components/ButtonRandomComponent.vue";
  import CreditsComponent from "@/components/CreditsComponent.vue";

  export default {
    name: "Home",
    components: {
      ButtonComponent,
      CreditsComponent,
    },
    data() {
      return {
        datos: [],
        hayDatos: false,
        ruta: "https://quote-garden.herokuapp.com/api/v3/quotes/random",
      };
    },
    mounted() {
      this.random();
    },
    methods: {
      random() {
        axios
          .get(`https://quote-garden.herokuapp.com/api/v3/quotes/random`)
          .then((response) => {
            setTimeout(() => {
              this.hayDatos = true;
            }, 3000);
            let data = response.data;
            this.datos = data.data[0];
          })
          .catch((error) => console.log("Error", error));
      },
      ejecutarRandom(value) {
        if (value) {
          this.random();
        }
      },
    },
  };
</script>

<style lang="scss">
  .spinner {
    min-height: 100vh;
    background: #eee;
    margin: auto;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .quotes {
    margin: 60px auto;
    width: 300px;
    .box-quotes {
      border-left: 6px solid #f7df94;
      p {
        margin-left: 50px;
      }
    }
    .box-author-quotes {
      margin-top: 70px;
      transition: 0.5s all;
      p {
        transition: 0.5s all;
        color: #4f4f4f;
        margin-left: 50px;
        font-weight: 700;
      }

      p.type {
        font-weight: 500;
        color: #828282;
        font-size: 12px;
      }
    }
    .box-author-quotes:hover {
      background: #333;
      p {
        color: #fff;
      }
    }
  }
  .enlace {
    text-decoration: none;
  }
</style>
