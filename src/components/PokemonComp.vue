<template>
    <div id="principal">
        <div class="card">
        <div class="card-image">
        <figure>
             <img :src="currentImg" alt="Placeholder image">
        </figure>
        </div>
             <div class="card-content">
                <div class="media">
                     <div class="media-left">                            
                    </div>
                <div class="media-content">
                <p class="title is-4">{{num}} - {{ upper(name)}}</p>
                <p class="subtitle is-6">{{ pokemon.type }}</p>
            </div>
        </div>

        <div class="content">  
            <button class="button is-medium" @click="mudar">Mudar sprite</button>        
        </div>
        </div>
        </div>

        </div>
</template>

<script>
import axios from 'axios';
export default {
    created: function() {
        axios.get(this.url).then(res =>{
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
            console.log(this.pokemon);
        })
    },
    data(){
        return {
            isfront: true,
            currentImg : '',
            pokemon: {
                type:'',
                front:'',
                back: ''
            }
        }
    },
    props: {
        num:Number,
        name:String,
        url: String
    },
    methods: {
            mudar: function() {
                if(this.isfront){
                    this.isfront = false;
                    this.currentImg = this.pokemon.back;
                }else{
                    this.isfront = true;
                    this.currentImg = this.pokemon.front;
                }

            }

        },
    setup() {
        function upper (value) {
            var  newName = value[0].toUpperCase()+value.slice(1);
            return newName
        }
        {
            return{ 
            upper
            }
        }
        
    }
}
</script>

<style>
    #principal {
         margin-top: 4px;
    }

</style>