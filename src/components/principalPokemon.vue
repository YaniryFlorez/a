<template>
<div class="container">
    <div class="juego">
        <div v-if="pantalla1" class="pantalla1" >

        <div class="datos">
           <h3>Puntaje:{{puntaje}}</h3>
           <h3>Intentos: {{intentos}}</h3>
        </div>
        <div class="imagenes">
            <imgPokemon :ideP="id1"/>
            <imgPokemon :ideP="id2"/>
            <imgPokemon :ideP="id3"/>
        </div>
        <div class="boton">
            <button class="btn" v-on:click="jugar()">Jugar</button>
        </div>
        </div>
        <div v-if="mensajeG" class="mensajeG">
            <h1>Tu puntaje{{puntaje}}</h1>
            <h1>Has Ganado el premio</h1>
            <button v-on:click="reiniciar()">Nuevo juego</button>
        </div>
        <div v-if="mensajeP" class="mensajeG">
            <h1>Tu puntaje{{puntaje}}</h1>
            <h1>Has Perdido el Premio</h1>
            <button v-on:click="reiniciar()">Nuevo juego</button>
        </div>
    </div>
    
</div>
</template>

<script>
import imgPokemon from '../components/imgPokemon.vue'
export default {
    components:{
        imgPokemon,

    },
    data(){
        return{
            puntaje:0,
            intentos:0,
            cantidadP:[],
            id1:0,
            id2:0,
            id3:0,
            pantalla1:true,
            mensajeG:false,
            mensajeP:false,
        }
    },
    methods:{
        jugar(){
            if(this.intentos===0){
                this.cantidadP=[]
                this.cantidadP.push(this.generarIds(this.cantidadP));
                this.cantidadP.push(this.generarIds(this.cantidadP));
                this.cantidadP.push(this.generarIds(this.cantidadP));
                this.cantidadP.push(this.generarIds(this.cantidadP));
                this.cantidadP.push(this.generarIds(this.cantidadP));
                this.cantidadP.forEach(a=>console.log(a));
            }
            this.id1=this.cantidadP[Math.floor(Math.random()*5)];
            this.id2=this.cantidadP[Math.floor(Math.random()*5)];
            this.id3=this.cantidadP[Math.floor(Math.random()*5)];
            this.puntaje= this.puntaje+this.calcularPuntaje();
            this.intentos=this.intentos+1;
            if(this.intentos===5 && this.puntaje<=4){
                console.log(this.intentos);
                console.log(this.puntaje);
                this.mensajeP=true;
                this.pantalla1=false;
            }else if(this.intentos===5 && this.puntaje>4){
                this.pantalla1=false;
                this.mensajeG=true;
            }


            
        },

        generarIds(ides){
            if(ides && ides.length>=0){
                let existe= false;
                let auxId=-1;
                do{
                    auxId=Math.floor(Math.random()*500)+1;
                    for(var i=0; i<ides.length; i++){
                        if(ides.at(i)===ides){
                            existe=true;
                            break;
                        }
                    }
                }while(existe);
                return auxId;

            }else{
                return Math.floor(Math.random() * 500) + 1;
            }
        },

     calcularPuntaje(){

        if(this.id1===this.id2===this.id3){
           console.log('es 5')
           return 5;
          }else if((this.id1===this.id2 || this.id1===this.id3)&&(this.id2!=this.id3)){
    return 2;
               }else if((this.id1===this.id2 || this.id2===this.id3)&&(this.id1!=this.id3)){
                 return 2;
               }else{
                   return 0;
            }
        },
      reiniciar(){
        this.pantalla1=true;
        this.mensajeG=false;
        this.mensajeP=false;
        this.puntaje=0;
        this.intentos=0;
        this.cantidadP=[];
        this.id1=0;
        this.id2=0;
        this.id3=0;
      },

    },
   
}
</script>

<style>
.container{
    display: flex;
    justify-content:center;
    align-items: center;
}
.datos{
    display: grid;
    grid-template-columns: repeat(2, 150px);
}
.imagenes{
    display: grid;
    grid-template-columns: repeat(3, 300px);

}
</style>