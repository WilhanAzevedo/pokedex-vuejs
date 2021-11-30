<!--eslint-disable-->
<template>
    <div id="app">
        <div class="column is-half is-offset-one-quarter">
            <div class="columns">
                <div class="column is-2">
                    <figure class="image is-128x128 img-poke">
                        <img src="./assets/pokebola.png" />
                    </figure>
                </div>
                <div class="column">
                    <section class="section">
                        <h7 class="subtitle" style="color:white; ">
                            <p>UNIVERSIDADE DO ESTADO DE MATO GROSSO</p>
                            <p>CAMPUS UNIVERSITÁRIO DE SINOP</p>
                            <p>FACULDADE UNEMAT</p>
                            <p>CURSO SISTEMAS DE INFORMAÇÃO</p>
                        </h7>
                    </section>
                    <section class="section cabecalho">
                        <h7 class="subtitle" style="color:white; ">
                            <p>Disciplina: TÓPICOS ESPECIAIS EM COMPUTAÇÃO APLICADA</p>
                            <p>Aluno: WILHAN AZEVEDO DIONIZIO </p>
                            <p>Professor: IVAN LUIZ PEDROSO PIRES </p>
                        </h7>
                    </section>
                </div>
                <div class="column is-2">
                    <figure class="image is-96x96 img-poke">
                        <img src="./assets/unemat.png" />
                    </figure>
                </div>  
            </div>
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

    .cabecalho {
        padding-top: 4% !important;
        padding-left: 10% !important;
        padding-right: 1px !important;
        padding-bottom: 1px !important;
        text-align: left !important;
        
    }

    .subtitle {
       font-size: 0.85rem !important;
    }
</style>