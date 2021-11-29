<!-- eslint-disable -->
<template>
    <div class="card-pokemon">
        <div :class="classCard" @click="openModal">
            <div class="card-image">
                <figure>
                    <img class="poke-img" :src="currentImg" alt="Placeholder image" />
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                    <div class="media-content">
                        <p class="title is-5">#{{ num }}-{{ name | upper }}</p>
                        <span :class="className1">{{ pokemon.type1 | tipoPTBR }}</span>
                        <span :class="className2" v-if="pokemon.type2">{{
                            pokemon.type2 | tipoPTBR
                            }}</span>
                    </div>
                </div>

                <div class="content"></div>
            </div>
        </div>

    </div>
</template>
<script>/* eslint-disable */
    // import Informacoes from "./Informacoes.vue";
    

    import axios from "axios";
    
    const tipos = {
        grass: tipo("grass"),
        poison: tipo("poison"),
        fire: tipo("fire"),
        flying: tipo("flying"),
        water: tipo("water"),
        bug: tipo("bug"),
        normal: tipo("normals"),
        electric: tipo("electric"),
        ground: tipo("ground"),
        fairy: tipo("fairy"),
        fighting: tipo("fighting"),
        psychic: tipo("psychic"),
        rock: tipo("rock"),
        ice: tipo("ice"),
        ghost: tipo("ghost"),
        dragon: tipo("dragon"),
        dark: tipo("dark"),
        steel: tipo("steel"),
    };

    function tipo(tipo) {
        return "tag is-" + tipo + " is-normal";
    }

    export default {
        created: function () {
            axios.get(this.url).then((res) => {
                this.pokemon.type1 = res.data.types[0].type.name;
                if (res.data.types[1]) {
                    this.pokemon.type2 = res.data.types[1].type.name;
                }
                this.pokemon.front = res.data.sprites.other.dream_world.front_default;
                this.pokemon.back = res.data.sprites.back_default;
                this.currentImg = this.pokemon.front;

                this.className1 = tipos[this.pokemon.type1];
                this.className2 = tipos[this.pokemon.type2];
                this.classCard = "card card-" + this.pokemon.type1;
                this.dados = res.data;
            });

        },
        data() {
            return {
                isFront: true,
                currentImg: "",
                className1: "",
                className2: "",
                classCard: "",
                pokemon: {
                    type: "",
                    front: "",
                    back: "",
                },
                dados: {},
            };
        },
        props: {
            num: Number,
            name: String,
            url: String,
        },
        filters: {
            upper: function (value) {
                return value[0].toUpperCase() + value.slice(1);
            },
            tipoPTBR: function (value) {
                switch (value) {
                    case "normal":
                        return "Normal";
                    case "fighting":
                        return "Lutador";
                    case "flying":
                        return "Voador";
                    case "poison":
                        return "Venenoso";
                    case "ground":
                        return "Terra";
                    case "rock":
                        return "Pedra";
                    case "bug":
                        return "Inseto";
                    case "ghost":
                        return "Fantasma";
                    case "steel":
                        return "Aço";
                    case "fire":
                        return "Fogo";
                    case "water":
                        return "Água";
                    case "grass":
                        return "Planta";
                    case "electric":
                        return "Elétrico";
                    case "psychic":
                        return "Psíquico";
                    case "ice":
                        return "Gelo";
                    case "dragon":
                        return "Dragão";
                    case "dark":
                        return "Sombrio";
                    case "fairy":
                        return "Fada";
                    default:
                        return "";
                }
            },
        },
        components: {

        },
        methods: {
            openModal: function () {
                this.$emit("open-modal", this.dados);
                //console.log(this.dados);
            },
        },
    };
</script>

<style>
    .card-pokemon {
        margin-top: 1rem;
        padding: 5px;
        
    }

    .card-pokemon:hover {
        transform: scale(1.1);
        
    }
    .poke-img {
        max-width: 128px;
        max-height: 128px;
        margin: 1rem;
        min-height: 128px;
        min-width: 128px;
    }

    
    .card-grass {
        background-color: #37ce2691 !important;
    }

    .card-fire {
        background-color: #f5a52391 !important;
    }

    .card-water {
        background-color: #4d9ef491 !important;
    }

    .card-electric {
        background-color: #f7d02c91 !important;
    }

    .card-fighting {
        background-color: #d5672391 !important;
    }

    .card-flying {
        background-color: #90ddf091 !important;
    }

    .card-poison {
        background-color: #b97fc991 !important;
    }

    .card-ground {
        background-color: #55351791 !important;
    }

    .card-rock {
        background-color: #62615c91 !important;
    }

    .card-bug {
        background-color: #c1d32f91 !important;
    }

    .card-normal {
        background-color: #a8a8a891 !important;
    }

    .card-ghost {
        background-color: #73579791 !important;
    }

    .card-ice {
        background-color: #51c4e791 !important;
    }

    .card-dragon {
        background-color: #5f030791 !important;
    }

    .card-dark {
        background-color: #1e142a91 !important;
    }

    .card-steel {
        background-color: #b7b7ce91 !important;
    }

    .card-fairy {
        background-color: #d685ad91 !important;
    }

    .card-psychic {
        background-color: #f15b8591 !important;
    }

    .is-grass {
        background-color: #37ce26 !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-fire {
        background-color: #f5a623 !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-water {
        background-color: #4d9ef4 !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-bug {
        background-color: #c1d32f !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-poison {
        background-color: #b97fc9 !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-electric {
        background-color: #f7d02c !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-ground {
        background-color: #553517 !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-flying {
        background-color: #90ddf0 !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-fighting {
        background-color: #d56723 !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-psychic {
        background-color: #f15b85 !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-rock {
        background-color: #62615c !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-ghost {
        background-color: #735797 !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-dragon {
        background-color: #5f0307 !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-dark {
        background-color: #1e1491 !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-steel {
        background-color: #b7b7ce !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-fairy {
        background-color: #d685ad !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-normals {
        background-color: #a8a8a8 !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }

    .is-ice {
        background-color: #51c4e7 !important;
        color: #fff !important;
        font-weight: 600;
        margin: 2px;
    }
</style>