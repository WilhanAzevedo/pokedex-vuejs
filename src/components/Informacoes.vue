<template>
    <div class="modal" :class="modal ? 'is-active' : ''">
        <div class="modal-background"></div>
        <div class="modal-card">
            <div class="card-image profile">
                <figure>
                    <img class="poke-img" v-if="modal" :src="dadosAll.sprites.other.dream_world.front_default"
                        alt="Placeholder image" />
                </figure>
                <!-- FUNÇÃO PENDENTE AINDA NAO FUNCIONA CORRETAMENTE -->
                <!-- <span class="icon next" :class="dadosAll.types[0].type.name == 'normal' ? 'btn-normals' : 'btn-'+dadosAll.types[0].type.name " @click="next">
                    <i class="fas fa-caret-right"></i>
                </span>
                <span class="icon previous" :class="dadosAll.types[0].type.name == 'normal' ? 'btn-normals' : 'btn-'+dadosAll.types[0].type.name " @click="previous">
                    <i class="fas fa-caret-left"></i>
                </span> -->
            </div>
                        
            <section class="modal-card-body">
                <button class="modal-close is-large custom-close" :class="dadosAll.types[0].type.name == 'normal' ? 'card-normals' : 'card-'+dadosAll.types[0].type.name " aria-label="close" @click="closeModal"></button>
                <div class="field topm">
                    <div class="field-body">
                        <div class="field">
                            <p class="control">
                                <span class="tag is-medium is-white is-rounded">{{dadosAll.name | upper }}</span>
                            </p>
                        </div>
                    </div>
                </div>
                <div class="field is-horizontal">
                    <div class="field-body">
                        <div class="field">
                            <p class="control">
                                <span class="tag is-medium is-white is-rounded">#{{dadosAll.id }}</span>
                            </p>
                        </div>
                    </div>
                </div>
                <div class="columns">
                    <div class="column">
                        <div class="field is-horizontal">
                            <div class="field-label is-normal">
                                 <label class="label">{{dadosAll.stats[0].stat.name | upper | statPTBR}}</label>
                            </div>
                            <div class="field-body">
                                <div class="field">
                                    <p class="control" style="top: 45%;">
                                        <progress class="progress is-primary is-normal show-value"
                                            :value="dadosAll.stats[0].base_stat" max="100"></progress>
                                    </p>
                                </div>
                            </div>
                        </div>
                        <div class="field is-horizontal">
                            <div class="field-label is-normal">
                                <label class="label">{{dadosAll.stats[1].stat.name | upper | statPTBR}}</label>
                            </div>
                            <div class="field-body">
                                <div class="field">
                                    <p class="control" style="top: 45%;">
                                        <progress class="progress is-link is-normal show-value" :value="dadosAll.stats[1].base_stat"
                                            max="100"></progress>
                                    </p>
                                </div>
                            </div>
                        </div>
                        <div class="field is-horizontal">
                            <div class="field-label is-normal">
                                <label class="label">{{dadosAll.stats[2].stat.name | upper | statPTBR}}</label>
                            </div>
                            <div class="field-body">
                                <div class="field">
                                    <p class="control" style="top: 45%;">
                                        <progress class="progress is-info is-normal show-value" :value="dadosAll.stats[2].base_stat"
                                            max="100"></progress>
                                    </p>
                                </div>
                            </div>
                        </div>
                        <div class="field is-horizontal">
                            <div class="field-label is-normal">
                                <label class="label">{{dadosAll.stats[3].stat.name | upper | statPTBR}}</label>
                            </div>
                            <div class="field-body">
                                <div class="field">
                                    <p class="control" style="top: 45%;">
                                        <progress class="progress is-success is-normal show-value"
                                            :value="dadosAll.stats[3].base_stat" max="100"></progress>
                                    </p>
                                </div>
                            </div>
                        </div>
                        <div class="field is-horizontal">
                            <div class="field-label is-normal">
                                <label class="label">{{dadosAll.stats[4].stat.name | upper | statPTBR}}</label>
                            </div>
                            <div class="field-body">
                                <div class="field">
                                    <p class="control" style="top: 45%;">
                                        <progress class="progress is-warning is-normal show-value"
                                            :value="dadosAll.stats[4].base_stat" max="100"></progress>
                                    </p>
                                </div>
                            </div>
                        </div>
                        <div class="field is-horizontal">
                            <div class="field-label is-normal">
                                <label class="label">{{dadosAll.stats[5].stat.name | upper | statPTBR }}</label>
                            </div>
                            <div class="field-body">
                                <div class="field">
                                    <p class="control" style="top: 45%;">
                                        <progress class="progress is-danger is-normal show-value"
                                            :value="dadosAll.stats[5].base_stat" max="100"></progress>
                                    </p>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                        <div class="column">
                            <div class="card-det">
                                <div class="card-details">
                                    <div class="card-content">
                                        <div class="media">
                                            <div class="media-content">
                                                <div class="field is-horizontal detalhes">
                                                    <div class="field-label is-normal">
                                                        <label class="label xp">XP</label>
                                                    </div>
                                                    <div class="field-body">
                                                        <div class="field">
                                                            <p class="control" style="top: 45%;">
                                                                <progress class="progress is-primary is-normal show-value" :value="dadosAll.base_experience" max="1000"></progress>
                                                            </p>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="field is-horizontal detalhes">
                                                    <div class="field-label is-normal">
                                                        <label class="label xp">Tipo</label>
                                                    </div>
                                                    <div class="field-body">
                                                        <div class="field">
                                                               <span class="tag is-normal is-rounded" v-for="(tipo, index) in this.dadosAll.types" :key="index" :class="tipo.type.name != 'normal' ? 'is-'+tipo.type.name : 'is-normals'">{{tipo.type.name | tipoPTBR}}</span>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                            </div>
                                        </div>
                                        <div class="content"></div>
                                    </div>
                                </div>
                            </div>
                            <div class="card-fra">
                                <div class="card-fraquezas">
                                    <div class="card-content">
                                        <div class="media">
                                            <div class="media-content">
                                                
                                                <p class="title is-4 fraquezas">Fraquezas</p>
                                                <span class="tag is-normal is-rounded" v-for="(name, index) in this.finalTipos" :key="index" :class="name != 'normal' ? 'is-'+name : 'is-normals'">{{name | tipoPTBR}}</span>
                                                
                                                
                                            </div>
                                        </div>
                                        <div class="content"></div>
                                    </div>
                                </div>
                            </div>
                            
                    </div>
                    
                </div>
                <div class="columns">
                    <div class=column>
                        <div class="card-det">
                            <div class="card-details">
                                <div class="card-content">
                                    <div class="media">
                                        <div class="media-content">
                                            <Evolucoes :especie="especies" :click="clc" @open-evolution="openEvolution"/>    
                                                  
                                        </div>
                                    </div>
                                    <div class="content"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </section>
        </div>
        <!-- <button class="modal-close is-large" aria-label="close" @click="closeModal"></button> -->
    </div>
</template>

<script>
    import Evolucoes from './Evolucoes.vue'
    import axios from "axios"; 
    

    export default {
        created() {

            for(let i = 0; i < this.dadosAll.types.length; i++){
                axios.get(this.dadosAll.types[i].type.url).then(res => {
                    this.typesDemage1.push(res.data.damage_relations);
                    if(this.dadosAll.types.length == i+1){
                        
                        this.getTipos(this.typesDemage1);
                        
                    }
                    
                });
            }
            console.log(this.dadosAll.especie);
            this.especies = this.dadosAll.species.url;
            
        },
        data() {
            return {
                dados: "",
                typesDemage1: [],
                typesDemage2: [],
                finalTipos: [],
                especies: "",
                clc: false,
            };
        },
        components: {
            Evolucoes,
        },
        props: {
            dadosAll: Object,
            modal: Boolean,
            demages: Array,
        },
        filters: {
            upper: function (value) {
                return value[0].toUpperCase() + value.slice(1);
            },
            statPTBR: function (value) {
                switch (value) {
                    case "Attack":
                        return "Ataque";
                    case "Defense":
                        return "Defesa";
                    case "Special-attack":
                        return "Ataque Especial";
                    case "Special-defense":
                        return "Defesa Especial";
                    case "Speed":
                        return "Velocidade";
                    case "Hp":
                        return "HP";
                    default:
                        return "";
                }
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
            }
        },
        methods: {
            closeModal() {

                this.$emit("close");
            },
            getTipos(tipos) {
                for (let i = 0; i < tipos.length; i++) {
                    for (let j = 0; j < tipos[i].double_damage_from.length; j++) {
                        if (tipos[i].double_damage_from[j].name != this.dadosAll.types[0].type.name) {
                                if(this.finalTipos.indexOf(tipos[i].double_damage_from[j].name) == -1){
                                    this.finalTipos.push(tipos[i].double_damage_from[j].name);
                                }
                        }
                        if(tipos.length > 1){
                            if (tipos[i].double_damage_from[j].name != this.dadosAll.types[1].type.name) {
                                if(this.finalTipos.indexOf(tipos[i].double_damage_from[j].name) == -1){
                                    this.finalTipos.push(tipos[i].double_damage_from[j].name);
                                }
                            }
                        }
                    }
                    for (let j = 0; j < tipos[i].half_damage_from.length; j++) {
                        let index = this.finalTipos.indexOf(tipos[i].half_damage_from[j].name);
                        if(index > -1){
                           this.finalTipos.splice(index, 1);
                        }
                    }
                    for (let j = 0; j < tipos[i].no_damage_from.length; j++) {
                        let index = this.finalTipos.indexOf(tipos[i].no_damage_from[j].name);
                        if(index > -1){
                           this.finalTipos.splice(index, 1);
                        }
                    }
                }
                
                for (let i = 0; i < tipos.length; i++) {
                    for (let j = 0; j < tipos[i].double_damage_to.length; j++) {
                        let index2 = this.finalTipos.indexOf(tipos[i].double_damage_to[j].name);
                        if(index2 > -1){
                           this.finalTipos.splice(index2, 1);
                        }
                    }
                }
            },
            openEvolution: function(evolution) {
                axios.get("https://pokeapi.co/api/v2/pokemon/"+evolution).then(res => {
                    this.$emit("open-evolution-info", res.data);
                });
            },
            next: function() {
                if(this.dadosAll.id != 151){
                    let id = this.dadosAll.id + 1;
                    axios.get("https://pokeapi.co/api/v2/pokemon/"+id).then(res => {
                    this.$emit("open-evolution-info", res.data);
                    for(let i = 0; i < this.dadosAll.types.length; i++){
                        axios.get(this.dadosAll.types[i].type.url).then(res => {
                            this.typesDemage1 = [];
                            this.finalTipos = [],
                            this.especies = "",
                            this.typesDemage1.push(res.data.damage_relations);
                            if(this.dadosAll.types.length == i+1){

                                //console.log(this.typesDemage1);
                        
                                this.getTipos(this.typesDemage1);
                        
                            }
                    
                        });
                    }
                    // console.log(this.dadosAll.especie);
                    this.especies = this.dadosAll.species.url;
                    this.clc =  true;
                    //this.clc =  false;
                    
                    
                });
                }else{
                    let id = 1;
                    axios.get("https://pokeapi.co/api/v2/pokemon/"+id).then(res => {
                    this.$emit("open-evolution-info", res.data);
                });
                }
            },
            previous: function() {
                if(this.dadosAll.id != 1){
                    let id = this.dadosAll.id - 1;
                    axios.get("https://pokeapi.co/api/v2/pokemon/"+id).then(res => {
                    this.$emit("open-evolution-info", res.data);
                });
                }else{
                    let id = 151;
                    axios.get("https://pokeapi.co/api/v2/pokemon/"+id).then(res => {
                    this.$emit("open-evolution-info", res.data);
                });
                }
                
            },
        },
    };
</script>

<style>

    /*btns*/
     .btn-grass {
        color: #37ce26 !important;
    }

    .btn-fire {
        color: #f5a523 !important;
    }

    .btn-water {
        color: #4d9ef4 !important;
    }

    .btn-electric {
        color: #f7d02c !important;
    }

    .btn-fighting {
        color: #d56723 !important;
    }

    .btn-flying {
        color: #90ddf0 !important;
    }

    .btn-poison {
        color: #b97fc9 !important;
    }

    .btn-ground {
        color: #553517 !important;
    }

    .btn-rock {
        color: #62615c !important;
    }

    .btn-bug {
        color: #c1d32f !important;
    }

    .btn-normal {
        color: #a8a8a8 !important;
    }

    .btn-ghost {
        color: #735797 !important;
    }

    .btn-ice {
        color: #51c4e7 !important;
    }

    .btn-dragon {
        color: #5f0307 !important;
    }

    .btn-dark {
        color: #1e142a !important;
    }

    .btn-steel {
        color: #b7b7ce !important;
    }

    .btn-fairy {
        color: #d685ad !important;
    }

    .btn-psychic {
        color: #f15b85 !important;
    }


    .next{
        font-size: 6em;
        color: #fff;
        margin-right: -420%;
    }

    .previous{
        font-size: 6em;
        color: #fff;
        margin-left: 0px;
    }

    button.modal-close.is-large.custom-close {
    position: absolute;
    right: auto;
    top: auto;
    margin-left: 47%;
    margin-top: -6%;
    }

    .modal-card{
        overflow: visible !important;
    }

    .profile {
        max-width: 160px;
        max-height: 160px;
        background-color: white;
        top: 5rem;
        border-radius: 50%;
        box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.75);
        margin: 0 auto;
    }

    .card-details {
        box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.75);
        border-radius: 15px;
        background-color: #292929 !important;
    }

    .card-fraquezas {
        margin-top: 10px;
        box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.75);
        border-radius: 15px;
        background-color: #f139396c !important;
    }

    .fraquezas {
        color: #ffffff !important;
        margin-top: -0.5rem !important;
        margin-bottom: 20px !important;
    }

    .modal-card-body {
        border-radius: 15px;
        background-color: #292929 !important;
    }

    .field-label .label {
        font-size: 12px !important;
        color: #fff !important;
        min-width: 62px;
    }

    .field-label .xp {
        font-size: 12px !important;
        color: #fff !important;
        min-width: 0px;
    }

    .detalhes {
    margin-bottom: 20px !important;
    }

    .topm {
        margin-top: 5rem;
    }

progress.show-value {
  position: relative;
}


progress.show-value:after {
  content: attr(value);
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  font-size: calc(1rem / 1.5);
  line-height: 1rem;
  font-weight: bold;
    color: #292929;
}

.progress.is-small+.progress-value {
  font-size: calc(0.75rem / 1.5);
  line-height: 0.75rem;
}

.progress.is-medium+.progress-value {
  font-size: calc(1.25rem / 1.5);
  line-height: 1.25rem;
}

.progress.is-large+.progress-value {
  font-size: calc(1.5rem / 1.5);
  line-height: 1.5rem;
}

.progress.is-normal+.progress-value {
  font-size: calc(1rem / 1.5);
  line-height: 0.75rem;
}
</style>