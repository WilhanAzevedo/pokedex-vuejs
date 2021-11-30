<!--eslint-disable-->
<template>
    <div id="app">
        <div class="column is-half is-offset-one-quarter">
            <figure class="image is-128x128 img-poke">
                <img src="./assets/pokebola.png" />
            </figure>

            <input class="input is-rounded" type="text" name="" id="" placeholder="Buscar pokemon pelo nome"
                v-model="busca" />
            <!-- <button id="btn-busca" class="button is-info is-fullwidth is-rounded">
                Buscar
            </button> -->
            <div class="columns is-multiline">
                <div class="column is-one-third" v-for="(poke, index) in resultadoBusca" :key="poke.url">
                    <Pokemon :name="poke.name" :url="poke.url" :num="index +1" @open-modal="openModal" />
                </div>
            </div>
        </div>
        <Informacoes v-if="isModal" :dadosAll="dadosTipo" :modal="isModal" :demages="demage" @close="closeModal"  @open-evolution-info="openEvolutionInfo"/>
    </div>
</template>

<script>
/* eslint-disable */

    import Pokemon from "./components/Pokemon.vue";
    import Informacoes from "./components/Informacoes.vue";
    import axios from "axios";

    export default {
        name: "App",
        data() {
            return {
                pokemons: [],
                demage: [],
                filteredPokemons: [],
                busca: "",
                dadosTipo: {},
                isModal: false,
            };
        },
        created: function () {
            axios
                .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
                .then((res) => {
                    this.pokemons = res.data.results;
                    this.filteredPokemons = res.data.results;
                });
        },
        components: {
            Pokemon,
            Informacoes,
        },
        methods: {
            buscar: function () {
                this.filteredPokemons = this.pokemons;
                if (this.busca == "" || this.busca == " ") {
                    this.filteredPokemons = this.pokemons;
                } else {
                    this.filteredPokemons = this.pokemons.filter(
                        (pokemon) => pokemon.name == this.busca
                    );
                }
            },
            openModal: function (params) {
                this.isModal = true;
                this.dadosTipo = params;
            },
            closeModal: function () {
                this.isModal = false;
                this.demage = [];
            },
            openEvolutionInfo: function (params) {
                this.dadosTipo = params;
            },
        },
        computed: {
            resultadoBusca: function(){
              if(this.busca == '' || this.busca == ' '){
                return this.pokemons;
            }else{
                var self=this;
              return this.pokemons.filter(function(pokemon){ 
                  return pokemon.name.toLowerCase().indexOf(self.busca.toLowerCase()) >=0;
                  }
                );
            }
          }
        },
    };
</script>


<style lang="scss">
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        background-color: #1a1d20;
    }

    #nav {
        padding: 30px;

        a {
            font-weight: bold;
            color: #2c3e50;

            &.router-link-exact-active {
                color: #42b983;
            }
            
        }
    }

    #btn-busca {
        margin-top: 2%;
        margin-bottom: 2%;
    }

    .img-poke {
        margin: 0 auto;
    }

    // .modal-card{
    //     width: 650px !important;
    // }
</style>