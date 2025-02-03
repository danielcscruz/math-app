<script setup>
import {reactive} from 'vue'

const estado = reactive({
  resposta: 0,
  numero1 : 0,
  numero2 : 0,
  operador: ''
})

function calcularOperacao(numa,numb,o){
  const a = Number(numa)
  const b = Number(numb)
  switch(o){
    case "+":  estado.resposta = a+b;  break;
    case "-":  estado.resposta = a-b;  break;
    case "*":  estado.resposta = a*b;  break;
    case "/":  estado.resposta = a/b;  break;
  }
  console.log(estado.resposta)
}

const atualizarVariaveis = (v,b) => {
  switch(b){
    case "1":
      estado.numero1 = v;
      calcularOperacao(estado.numero1, estado.numero2, estado.operador);
      break;
    case "2":
      estado.numero2 = v;
      calcularOperacao(estado.numero1, estado.numero2, estado.operador);
      break;  
  }
}


const mudarOperador = (o) => {
  estado.operador = o;
  console.log(o);
  calcularOperacao(estado.numero1, estado.numero2, estado.operador);
}

const limparTela = () =>{
  estado.operador = '';
  estado.numero1 = 0;
  estado.numero2 = 0;
}


</script>

<template>
<div class="container">
  <div class="calculator pt-5 d-flex flex-column align-items-center ">
    <div class="dis pe-5 ps-5 w-50 py-4 rounded-3 text-light text-center col-md-5">
      <h5 v-if="estado.operador ===''">math app</h5>
      <h5 v-else="estado.operador ===''">{{  estado.numero1 }} <span v-if="estado.numero1 !== '' && estado.numero2 !== ''">{{ estado.operador }}</span>  {{ estado.numero2 }} <span v-if="estado.numero1 !== '' && estado.numero2 !== ''" >=</span></h5>
      
      <h1 v-if="estado.operador ===''" style="color:#505050">__</h1>
      <h1 v-else="estado.operador ===''">{{ estado.resposta }}</h1>

    </div>
    <div class="numbers mt-5 d-flex justify-content-center align-items-center "> 
      <input type="number" class="fs-1 py-4 rounded-4 col-md-2 col-sm-4 ms-5 me-5 bg-light"
      v-model="estado.numero1" @keyup="atualizarVariaveis($event.target.value,'1')" >
      <!-- <span class="operator fs-1">{{ estado.operador }}</span> -->
      <select v-model="estado.operador" @change="mudarOperador($event.target.value)" class="form-control">
                    <option value=""></option>
                    <option value="+">+</option>
                    <option value="-">-</option>
                    <option value="/">/</option>
                    <option value="*">*</option>
      </select>
      <input type="number" class="fs-1 py-4 rounded-4 col-md-2 col-sm-4 ms-5 me-5 bg-light" 
      v-model="estado.numero2" @keyup="atualizarVariaveis($event.target.value,'2')">
    </div>
    <div class="operators p-5 mb-4 mt-4 d-flex justify-content-center">
      <form @submit.prevent="calcularOperacao(estado.numero1,estado.numero2,estado.operador)">
        <button type="button" class="fs-1 ms-3 me-3 p-4 rounded-5" @click="limparTela()">C</button>
        
      </form>
    </div>
  </div>
</div>

</template>

<style scoped>

*{
  border: 0;
  padding: 0;
  box-sizing: border-box;
}

select{
  width: 45px;
  text-align: center;
  background-color: transparent;
  color: white;
  font-size: 20px;
}
select:hover{
  cursor: pointer;
  background-color: #ffaa50;
}

select:active{
  background-color: transparent;
}
select::selection{
  background-color: transparent;
}

button{
  background-color: #FE941F;
  color: #292929;
  cursor: pointer;
}

button:hover{
  background-color: #ffaa50;
}


input{
  text-align: center;
}

.container{
  background-color: #22252D;
}

.dis{
  background-color:#505050 ;
  
}
.operator{
  color: silver;
}

h5{
  text-align: end;
  font-weight: 100;
}
input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

input[type="number"] {
  -moz-appearance: textfield;
}
</style>
