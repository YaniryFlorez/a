<template>
<div class="container">
    <div class="juego">
     <div v-if="mostrarPP" class="pantallaP">
           <div class="datos">
             <h3>Puntaje:{{punt}}</h3>
             <h3>Intentos:{{intent}}</h3>
           </div>
           <div class="ver">
              <imagen :imagen="foto[0]" :nombre="nombres[0]"/>
              <imagen :imagen="foto[1]" :nombre="nombres[1]"/>
              <imagen :imagen="foto[2]" :nombre="nombres[2]"/>
           </div>

           <div class="boton">
             <button v-on:click="jugar()">Jugar</button>
           </div>
       </div>
       
    <div v-if="mostrarP" class="mensajes">
        <h1>Has usado 5 intentos</h1>
        <h1>Juego Tetminado, Vuelve a intetar</h1>
        <button v-on:click="reiniciar()">Nuevo juego</button>
    </div>

    <div v-if="mostrarG" class="mensajes">
        <h1>Tu puntaje{{punt}}</h1>
        <h1>Has Ganado el premio</h1>
        <button v-on:click="reiniciar()">Nuevo juego</button>
    </div>
</div>

</div>

</template>



<script>
import imagen from '../components/imagen.vue';

export default {
    components:{
        imagen

    },
    data(){

        return{
            punt:0,
            intent:0,
            mostrarP: false,
            mostrarG: false,
            mostrarPP: true,
            foto:['https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg',
                    'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/2.svg',
                    'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/3.svg'
            ],
            nombres:['xxxxx','xxxxx','xxxxx']
        }
  },
  methods:{
    async jugar(){
        
        if(this.intent<=5){
         for(let i=0; i<3; i++){
         const { answer, image } = await fetch("https://yesno.wtf/api").then((respuesta) => respuesta.json());
         this.foto[i]=image;
         this.nombres[i]=answer;
          }
        }
       const contadorSi=this.nombres.filter((respuesta)=>respuesta==="yes").length;

       if(contadorSi===3){
           this.punt+=5;
           console.log("5");
         }else if(contadorSi===2){
            console.log("2");
        this.punt+=2;
           }else if(contadorSi===1){
            console.log("1");
               this.punt+=1;
               }
               this.intent++;

        if(this.intent===5 && this.punt<10){
            this.mostrarP=true;
            this.mostrarPP=false;
        }
        if(this.punt>=10){
            this.mostrarG=true;
            this.mostrarPP=false;
        }

        

     },
     reiniciar(){
        this.mostrarPP =true;
        this.mostrarG=false;
        this.mostrarG=false;
        this.punt=0,
            this.intent=0,
            this.foto=['https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg',
                    'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/2.svg',
                    'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/3.svg'
            ],
            this.nombres=['xxxxx','xxxxx','xxxxx']
     }
    }
  }

</script>



<style>
.container{
    display: flex;
    align-items: center;
    justify-content: center;
   
}
.pantallaP{
    display:inline;
    align-items: center;
    justify-content: center;
   
}
.datos{
    display: flex;
    align-content: center;
    gap: 40px;
}
.ver{
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 40px;

}
.juego{
    display: flex;
    flex-direction:column;
    align-items: center;
    justify-content: center;
}
</style>