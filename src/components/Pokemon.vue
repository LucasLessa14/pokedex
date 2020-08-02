<template>
<div id="pokemon">
    <div class="card">
    <div class="card-image">
        <figure>
            <img :src="currentImgBack" alt="Placeholder image">
            <img :src="currentImgFront" alt="Placeholder image">
        </figure>
    </div>
    <div class="card-content">
        <div class="media">
        <div class="media-content">
            <p class="title is-4">{{name | upper}}</p>

            <div v-for="type in pokemon.types" :key="type" class="type">
                <span :class="{'tag is-success': type === 'grass',
                                'tag is-warning': type === 'electric',
                                'tag is-danger': type === 'fire',
                                'tag is-link': type === 'water',
                                'tag is-poison': type === 'poison',
                                'tag is-ground': type === 'ground',
                                'tag is-primary': type === 'psychic',
                                'tag is-normal': type === 'normal',
                                'tag is-fighting': type === 'fighting',
                                'tag is-rock': type === 'rock',
                                'tag is-ghost': type === 'ghost',
                                'tag is-info': type === 'ice',
                                'tag is-flying': type === 'flying',
                                'tag is-light': type === 'steel',
                                'tag is-fairy': type === 'fairy',
                                'tag is-bug': type === 'bug',
                                'tag is-dragon': type === 'dragon'}">{{type}}</span>
            </div>
        </div>
        </div>

        <div class="content">
            <button class="button is-fullwidth is-danger" @click="mudarSprite">{{textButton}}</button>
        </div>
    </div>
    </div>
</div>
</template>

<script>
import axios from 'axios';
export default {
    created: function() {
        axios.get(this.url).then(res => {
            res.data.types.forEach(element => this.pokemon.types.push(element.type.name));
            this.pokemon.frontDefault = res.data.sprites.front_default;
            this.pokemon.backDefault = res.data.sprites.back_default;
            this.pokemon.frontShiny = res.data.sprites.front_shiny;
            this.pokemon.backShiny = res.data.sprites.back_shiny;
            this.currentImgFront = this.pokemon.frontDefault;
            this.currentImgBack = this.pokemon.backDefault;
        })
    },
    data(){
        return {
            isShiny: false,
            currentImgFront: '',
            currentImgBack: '',
            textButton: 'Modo Normal',
            pokemon: {
                types: [],
                front: '',
                back: ''
            }
        }
    },
    props: {
        name: String,
        url: String
    },
    filters: {
        upper: function(value) {
            var newName = value[0].toUpperCase() + value.slice(1);
            return newName;
        }
    },
    methods: {
        mudarSprite: function() {
            if(this.isShiny) {
                this.isShiny = false;
                this.currentImgFront = this.pokemon.frontDefault;
                this.currentImgBack = this.pokemon.backDefault;
                this.textButton = "Modo Normal";
            } else {
                this.isShiny = true;
                this.currentImgFront = this.pokemon.frontShiny;
                this.currentImgBack = this.pokemon.backShiny;
                this.textButton = "Modo Brilhante";
            }
        }
    }
}
</script>

<style>
    #pokemon {
        margin-top: 2%;
    }

    span {
        margin: 0 5px;
    }

    .tag {
        font-weight: bold;
    }

    .tag:not(body).is-poison {
        background-color: purple;
        color: white;
    }

    .tag:not(body).is-ground {
        background-color: #885744;
        color: white;
    }

    .tag:not(body).is-normal {
        background-color: brown;
        color: white;
    }

    .tag:not(body).is-rock {
        background-color: gray;
        color: white;
    }

    .tag:not(body).is-ghost {
        background-color: #993399;
        color: white;
    }

    .tag:not(body).is-fairy {
        background-color: hotpink;
        color: white;
    }

    .tag:not(body).is-bug {
        background-color: olivedrab;
        color: white;
    }

    .tag:not(body).is-flying {
        background-color: skyblue;
        color: whitesmoke;
    }

    .tag:not(body).is-fighting {
        background-color: darkkhaki;
        color: white;
    }

    .tag:not(body).is-dragon {
        background-color: pink;
        color: white;
    }

    .type {
        display: inline-block;
    }
</style>