<script setup>
import {ref,computed} from 'vue'
console.clear();
const name="Vue dinamico";
const styleColor="color: white";
const array=["blue","red","green"];
const activo=false;
//const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"];
const arrayFrutas = [
        {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
        },
    ];

    const objetoFruta={
      name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
            id:1
    };

    const arrayFrutas1=[
    {
        name: "Manzana",
        price: "$1.00",
        description: "Una manzana",
        stock: 0,
    },
    {
        name: "Pera",
        price: "$2.00",
        description: "Una pera",
        stock: 10,
    },
    {
        name: "Naranja",
        price: "$3.00",
        description: "Una naranja",
        stock: 20,
    },
];

//Metodos
const presiONA =()=>{
  console.log("Hola mundo como estan");
}
const presiONA1 =()=>{
  console.log("Hola mundo como estan mas avanzado");
}

const presiONA2=(parametro)=>{
  console.log(parametro);
}

// A partir de aqui usamos la reactividad
  const counter=ref(0);
  const increment=()=>{
    counter.value++;
  }

  //Practica
/*Agrega un botón para disminuir el contador.
Agrega un botón para resetear el contador.
Pinta el contador en rojo cuando el valor sea menor a cero.
Pinta el contador en verde cuando el valor sea mayor a cero.*/
  const contadornegativo=ref(0);
  const decrement=()=>{
    contadornegativo.value--;
  }
  const reset=()=>{
    contadornegativo.value=0;
  }
  const increment2=()=>{
    contadornegativo.value++;
  }


    const classCounter=computed(()=>{
      if(contadornegativo.value===0){
        return 'zero';
      }
      if(contadornegativo.value>0){
        return 'positive'
      }
      if(contadornegativo.value<0){
        return 'negative'
      }
    })

    //Practica 2
  /*Agrega un array y su respectivo método y botón add para almacenar los números favoritos del usuario.
  Pinta ese array utilizando v-for.
  Utiliza :disabled en el botón add, para que solo se pueda presionar si el array no contiene números repetidos. (utiliza una propiedad computada).*/
  const arrayUser=ref([])
  
  const agregarNUm=()=>{
    let bandera=true;
    for (let i=0;i<arrayUser.length;i++){
      if(arrayUser[i]===contadornegativo.value){
        bandera=false;
      }
    }
    if(bandera){
      arrayUser.value.push(contadornegativo.value);
    }
    ordenamientoArray();
  }
  const ordenamientoArray=()=>{
       arrayUser.value.sort(function (a,b) {return a-b  });
    }
 

  const bloquearBtnAdd=computed(()=>{
    const numSearch=arrayUser.value.find(num=>num===contadornegativo.value)
    if(numSearch===0)return true;
    return numSearch?true:false;
  })

</script>

<template>

  <div class="container text-center mt-3"> 
    <h1>Goalll {{name.toUpperCase()}}</h1>
  <h2>{{array}}</h2>
  <h2 :style="`color:${array[1]}`">Soy rojo</h2>
  <h2> {{activo ? "Estoy activo":"Estoy inactivo"}}</h2>
  <h2 v-if="activo===true">Estoy activo</h2>
  <p v-else-if="activo === false">Estoy inactivo</p>
  <ul >
    <li v-for="fruta in arrayFrutas" :key="fruta.name">
  {{fruta.name}} -{{fruta.description}}-{{fruta.price}}  
    </li>
  </ul>

  <ul>
    <li v-for="(value, propiedad,index) of objetoFruta" :key="value">
      {{index}}-{{value}}:{{propiedad}}
    </li>
  </ul>

  <ul>
    <li 
    v-if="activo"
    v-for="item in arrayFrutas1" 
    :key="item.name">
      {{item.name}}-{{item.price}}
    </li>
  </ul>

  <template v-for="item in arrayFrutas1"
  :key="item.name">
    <li v-if="item.stock>0">
    {{item.name}}-{{item.description}}
    </li>
  </template>
  
  <button v-on:click="presiONA()"> Activame-Sin parametros</button>
  <button @click="presiONA1"> Activame</button>
  <button @click="presiONA2(' Soy capaz de aprender Vue3')">Bton con parametro</button>
  <button @click.right.prevent="presiONA2(' Boton derecho')">Activame Right</button>
  <button @click="presiONA2(' Boton izquierdo')">Activame Left</button>
  <button @click.middle="presiONA2(' Boton del medio')">Activame Middle</button>

  <button @click="increment">Aumentar</button>
  <h2 >{{counter}}</h2>
  <h2>Practica</h2>
  <div class="btn-group">
  <button @click="increment2" class="btn btn-success">Aumentar contador</button>
  <button @click="decrement" class="btn btn-danger">disminuir contador</button>
  <button @click="reset" class="btn btn-secondary">Resetear contador</button>
  <button @click="agregarNUm" :disabled="bloquearBtnAdd" class="btn btn-primary">Agregar numero</button>
  </div>
  
  <h2 :class="classCounter">{{contadornegativo}}</h2>
  <ul class="list-group mt-4">
    <li 
    class="list-group-item"
    v-for="(num,index) in arrayUser" :key="index">
      {{num}}
    </li>
  </ul>

  <h1>Final del proyecto</h1>

  </div>

  

</template>

<style>
h1{
  color: blue;
}
.positive{
  color:aqua
}
.negative{
  color:red
}
.zero{
  color: tomato
}

</style>


