<template>
    <div class=columns>
        <div class="column">
            <div class="base" @click="openEvolution(evolucoes.base.id)">
                <figure>
                    <img class="poke-ev-img" :src="evolucoes.base.front" alt="Placeholder image"/>
                </figure>
            </div>
        </div>
        <div class="column is-1 seta">
            <span class="icon has-text-info ic">
                <i class="fas fa-2x fa-angle-double-right"></i>
            </span>
        </div>
        <div class="column">
            <div class="primeira" @click="openEvolution(evolucoes.primeira.id)">
                 <figure>
                    <img class="poke-ev-img" :src="evolucoes.primeira.front" alt="Placeholder image" />
                </figure>
            </div>
        </div>
        <div class="column is-1 seta">
            <span class="icon has-text-info ic">
                <i class="fas fa-2x fa-angle-double-right"></i>
            </span>
        </div>
        <div class="column">
            <div class="segunda" @click="openEvolution(evolucoes.segunda.id)">
                <figure>
                    <img class="poke-ev-img" :src="evolucoes.segunda.front" alt="Placeholder image" />
                </figure>
            </div>
        </div>
        <input type="hidden" v-if="click" v-model="atualizarr"/>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    created() {
        axios.get(this.especie).then(res => {
            axios.get(res.data.evolution_chain.url).then(res => {
                this.evolucoes.base.name = res.data.chain.species.name;
                this.evolucoes.base.id = res.data.chain.species.url.split('/')[6];
                axios.get(res.data.chain.species.url.replace('-species', '')).then(res =>{
                    this.evolucoes.base.front = res.data.sprites.other.dream_world.front_default;
                });
                
                if(res.data.chain.evolves_to.length > 0){
                    this.evolucoes.primeira.name = res.data.chain.evolves_to[0].species.name;
                    this.evolucoes.primeira.id = res.data.chain.evolves_to[0].species.url.split('/')[6];
                    axios.get(res.data.chain.evolves_to[0].species.url.replace('-species', '')).then(res =>{
                        this.evolucoes.primeira.front = res.data.sprites.other.dream_world.front_default;
                    });
                    if(res.data.chain.evolves_to[0].evolves_to.length > 0){
                        this.evolucoes.segunda.name = res.data.chain.evolves_to[0].evolves_to[0].species.name;
                        this.evolucoes.segunda.id = res.data.chain.evolves_to[0].evolves_to[0].species.url.split('/')[6];
                        axios.get(res.data.chain.evolves_to[0].evolves_to[0].species.url.replace('-species', '')).then(res =>{
                            this.evolucoes.segunda.front = res.data.sprites.other.dream_world.front_default;
                        });
                    }
                }
            });
        });
        console.log(this.click);
        //this.click = false;
             
    },
    data() {
        return {
            evolucoes: {
                base:{
                    name: '',
                    front: '',
                    id: ''
                },
                primeira:{
                    name: '',
                    front: '',
                    id: ''
                },
                segunda:{
                    name: '',
                    front: '',
                    id: ''
                }
            },                
        };
    },

    props: {
        especie: String,
        click: Boolean
    },
    filters: {
        upper: function (value) {
            return value[0].toUpperCase() + value.slice(1);
        },
    },
    methods: {
        openEvolution: function (id) {
            this.$emit('open-evolution', id);
        },
        atualizar: function () {
            this.evolucoes.base.name = '';
            this.evolucoes.base.front = '';
            this.evolucoes.base.id = '';
            this.evolucoes.primeira.name = '';
            this.evolucoes.primeira.front = '';
            this.evolucoes.primeira.id = '';
            this.evolucoes.segunda.name = '';
            this.evolucoes.segunda.front = '';
            this.evolucoes.segunda.id = '';
            axios.get(this.especie).then(res => {
            axios.get(res.data.evolution_chain.url).then(res => {
                this.evolucoes.base.name = res.data.chain.species.name;
                this.evolucoes.base.id = res.data.chain.species.url.split('/')[6];
                axios.get(res.data.chain.species.url.replace('-species', '')).then(res =>{
                    this.evolucoes.base.front = res.data.sprites.other.dream_world.front_default;
                });
                
                if(res.data.chain.evolves_to.length > 0){
                    this.evolucoes.primeira.name = res.data.chain.evolves_to[0].species.name;
                    this.evolucoes.primeira.id = res.data.chain.evolves_to[0].species.url.split('/')[6];
                    axios.get(res.data.chain.evolves_to[0].species.url.replace('-species', '')).then(res =>{
                        this.evolucoes.primeira.front = res.data.sprites.other.dream_world.front_default;
                    });
                    if(res.data.chain.evolves_to[0].evolves_to.length > 0){
                        this.evolucoes.segunda.name = res.data.chain.evolves_to[0].evolves_to[0].species.name;
                        this.evolucoes.segunda.id = res.data.chain.evolves_to[0].evolves_to[0].species.url.split('/')[6];
                        axios.get(res.data.chain.evolves_to[0].evolves_to[0].species.url.replace('-species', '')).then(res =>{
                            this.evolucoes.segunda.front = res.data.sprites.other.dream_world.front_default;
                        });
                    }
                }
            });
        });

        }
                
    },
    computed: {
        atualizarr: function () {
            if(this.click){
                this.atualizar();
            }
             
            return null;
        }
    }
};

</script>

<style>

.base{
    background-color: #f5f5f5;
    border-radius: 50%;
    padding: 10px;
    margin: 10px;
    width: 100px;
    height: 100px;
}

.primeira{
    background-color: #f5f5f5;
    border-radius: 50%;
    padding: 10px;
    margin: 10px;
    width: 100px;
    height: 100px;
}

.segunda{
    background-color: #f5f5f5;
    border-radius: 50%;
    padding: 10px;
    margin: 10px;
    width: 100px;
    height: 100px;
}

.poke-ev-img{
    max-width: 90px;
    max-height: 90px;
}

.ic{
    margin-top: 200%;
}
</style>