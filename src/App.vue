<script setup>
import { ref, computed } from 'vue'
const saludo="Hola";
const name="Vue dinamico";
const styleColor="color: blue";
const arrayColores = [ "red", "blue","orange","purple" ];
const activo ="";
const arrayFavoritos = ref([]);

const add = ()=> {
  arrayFavoritos.value.push(counter.value);
}

const frutas =[

      {
          name:"Manzana",
          price:"1500",
          description:"Una manzana",  
          id:2,
      },
      {
        name:"Pera",
          price:"2000",
          description:"Una pera",  
          id:25,
      },
      {
        name:"Naranja",
          price:"3050",
          description:"Una naranja",  
          id:38,
      },
];

const objetoPersona = {
   name :"Yair",
   surname : "Rodriguez",
   career :"ING de sistemas",
   age :18

}

const click = () => {
  console.log('Bobo catrehijueputa');

}
const counter =ref(0);

const incremento = ()=>{
  counter.value++;
}

const decremento = ()=> {
  counter.value --; //se coloca .value porque vue devuelve un objeto. para acceder se usa el .value
}
const recetear = ()=>{
  counter.value = 0;
}

const classCounter = computed(() =>{
  if(counter.value === 0){
    return 'zero'
  }

  if(counter.value > 0){
    return 'positivo'
  }

  if(counter.value <= 0 ){
    return 'negativo'
  }
  return''
});
//funcion para incluir numeros dentro de un array
const bloquearBtnAdd = computed(() =>{
    const  numSearch = arrayFavoritos.value.find(num => num === counter.value);
    console.log(numSearch);
    if(numSearch == 0){
      return true;
    }
    return numSearch ? true : false;
})
</script>

<template>
  <h1>{{ saludo }} {{ name.toUpperCase() }}</h1> <br>
  <h2 v-bind:style = "styleColor">Soy azul</h2>

  <p v-if="activo == true">Estoy activo</p>
  <p v-else-if="activo === false">Estoy inactivo</p>
  <p v-else>Estoy indeciso</p>


 <!-- recorrer un array -->

  <div v-for="(colorMostrar,index) in arrayColores" :key="index">
    color: {{ colorMostrar }}
  </div>
  <br><br><br><br>


  <!-- recorrer un objeto -->
 <ul>
  <li v-for="(value,propiedad) in objetoPersona" :key="value">
    {{ propiedad }} :  {{ value }}</li>
 </ul>

 <!-- mostrar un array de objetos usando condicionales-->
 <ul>
  <li class="siuu" v-for="(fruta, index) in frutas" :key="index">
     <p v-if="fruta.price > 12000">
      
      name: {{ fruta.name }} <br>
      description: {{ fruta.description }} <br>
      price: {{ fruta.price }} <br>
      id: {{ fruta.id }}
      
    </p>
    <p v-else>
      name: {{ fruta.name }} <br>
      description: {{ fruta.description }} <br>
      id: {{ fruta.id }}
    </p>
  </li>
 </ul>

 <!-- eventos -->
<button v-on:click="click">Activame 1 </button>
<button @click="click">Activame 2</button>

<br><br><br><br><br>
<button @click="incremento">Aumentar</button>
<button @click="decremento">Decrementar</button><br>
<div >
  <button class="recetear" @click="recetear">Recetear</button>
</div>
<h1 :class="classCounter">{{ counter }}</h1>

<button :disabled="bloquearBtnAdd" @click="add">Add</button>
{{ arrayFavoritos }}
<ul>
  <li v-for="(array,index) in arrayFavoritos" :key="index">
    {{ array }}
  </li>
</ul>
</template>

<style scoped>

.siuu{
  background-color: bisque;
  color: black;
}
.siuu:hover{
  color:red;
}
button{
  height: 20px;
  width: 90px;
}
.recetear{
      margin: 4px;
      padding: 3px;
      border: 10px;
      color:brown;
}
.recetear:hover{
  color:blueviolet;
  background-color: violet;
}
.positivo{
  color:green;
}
.negativo{
  color:red;
}
</style>
