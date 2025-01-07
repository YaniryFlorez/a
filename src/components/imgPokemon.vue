<template>
    <div class="container">
    <div>
        <img :src="optenerImagP" alt="no hay imagen">
    </div>
    <div>
        <h3>{{nombrePN}}</h3>
    </div>
</div>
  
</template>


<script>
export default {
    data() {
        return {
           apiDatos:'https://pokeapi.co/api/v2/pokemon/id',
           imagenN:require("../assets/imagen2.png"),
           nombrePN:"XXXXXXX",
    
        }
    },
    props:{
        ideP:Number,
        nombreP:String,

    },

    methods:{

        async optenerNombreP(){
            if(this.ideP && this.ideP>=0){
                console.log('no encontro');
                let url= this.apiDatos.replace("id",this.ideP);
                const respuesta= await fetch(url);
                const respuestaJson= await respuesta.json();
                this.nombrePN= respuestaJson.name;
                
            }else{
                this.nombreP=this.nombrePN;
            }

        },   
    },
    computed:{
        optenerImagP(){
            if(this.ideP && this.ideP>=0){
                return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.ideP}.svg`;
        }else{
            return this.imagenN;
        }
        
    },
  

},

watch: {
        ideP() {
            this.optenerNombreP();
        }
    },
 
    mounted() {
        this.optenerNombreP();
    }
}
</script>


<style>

</style>