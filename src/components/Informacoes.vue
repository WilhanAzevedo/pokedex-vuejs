<template>
    <div class="modal" :class="modal ? 'is-active' : ''">
        <div class="modal-background"></div>
        <div class="modal-card">
            <div class="card-image profile">
                <figure>
                    <img class="poke-img" v-if="modal" :src="dadosAll.sprites.other.dream_world.front_default"
                        alt="Placeholder image" />
                </figure>
            </div>
            <section class="modal-card-body">
                <div class="field topm">
                    <div class="field-body">
                        <div class="field">
                            <p class="control">
                                <span class="tag is-medium is-primary is-rounded">{{dadosAll.name | upper }}</span>
                            </p>
                        </div>
                    </div>
                </div>
                <div class="field">
                    <div class="field-body">
                        <div class="field">
                            <p class="control">
                                <span class="tag is-medium is-primary is-rounded">{{dadosAll.base_experience }}</span>
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
                        <!-- <div v-for="(dem, index) in ajustaTipos" :key="index">
                            <span class="tag is-info" >{{dem.name}}</span>
                        </div> -->
                        <!-- <span class="tag is-medium is-primary is-rounded">{{ajustaTipos}}</span> -->
                    </div>
                </div>
            </section>
        </div>
        <button class="modal-close is-large" aria-label="close" @click="closeModal"></button>
    </div>
</template>

<script>
    import axios from "axios"; 
    

    export default {
        created() {
            for(let i = 0; i < this.dadosAll.types.length; i++){
                axios.get(this.dadosAll.types[i].type.url).then(res => {
                    console.log(res.data.damage_relations.double_damage_from);
                    this.typesDamage.concat(res.data.damage_relations.double_damage_from);
                    
                });
            }
            console.log(this.typesDamage);
        },
        data() {
            return {
                dados: "",
                typesDamage: [],
            };
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
        },
        methods: {
            closeModal() {
                this.$emit("close");
            }
        },
        computed: {
            ajustaTipos: function () {
                
                return this.demages
            },
            
        },
    };
</script>

<style>
    .profile {
        max-width: 152px;
        max-height: 152px;
        background-color: white;
        top: 5rem;
        border-radius: 50%;
        box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.75);
        margin: 0 auto;
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