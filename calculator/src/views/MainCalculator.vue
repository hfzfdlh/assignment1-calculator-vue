<script setup>
import { ref } from 'vue'

const input = ref('')
const inputArr = ref([])


const calculationProcess = () =>{
    let curr = 0;
    let temp = '';

    let processObj = {
        '+':(a,b)=>{
            return a+b
        },
        '-':(a,b)=>{
            return a-b
        },
        'x':(a,b)=>{
            return a*b
        },
        '/':(a,b)=>{
            return a/b
        }

    }
    for (let i  = 0; i < inputArr.value.length-1; i = i+2){
        let a = inputArr.value[i]
        let b = inputArr.value[i+2]
        let proc = inputArr.value[i+1]
        curr = processObj[proc](a,b)
        console.log(a,b,proc,i, curr)
        inputArr.value[i+2] = curr

    }
    console.log(curr)
    inputArr.value =[curr]
    input.value = String(curr)
}

function addSymbol(char){
    // console.log(char)
    const keys = ['+','-','x','/']
    if (inputArr.value.length % 2 == 0 && keys.includes(char)){
        input.value = "Input Invalid"
    } else if (inputArr.value.length % 2 != 0 && !isNaN(Number(char))){
        input.value = "Input Invalid"
    } else{
        input.value += char
        inputArr.value.push(char)
    }
    
    // console.log(inputArr.value)
    
}

function clearValue(){
    inputArr.value=[]
    input.value = ''
}
</script>

<template>
    <div class="container">
        <div class="mainView">{{ input ? input: 0 }}</div>
        <div class="buttonTop">
            <div>
                <button @click="addSymbol('+')">+</button>
            </div>
            <div>
                <button @click="addSymbol('-')">-</button>
            </div>
            <div>
                <button @click="addSymbol('x')">x</button>
            </div>
            <div>
                <button @click="addSymbol('/')">/</button>
            </div>
        </div>
        <div class="buttonBottom">
            <div>
                <button @click="addSymbol('1')">1</button>
            </div>
            <div>
                <button @click="addSymbol('2')">2</button>
            </div>
            <div>
                <button @click="addSymbol('3')">3</button>
            </div>
            <div>
                <button @click="addSymbol('4')">4</button>
            </div>
            <div>
                <button @click="addSymbol('5')">5</button>
            </div>
            <div>
                <button @click="addSymbol('6')">6</button>
            </div>
            <div>
                <button @click="addSymbol('7')">7</button>
            </div>
            <div>
                <button @click="addSymbol('8')">8</button>
            </div>
            <div>
                <button @click="addSymbol('9')">9</button>
            </div>
            <div>
                <button @click="addSymbol('0')">0</button>
            </div>
            <div>
                <button @click="addSymbol('.')">.</button>
            </div>
            <div>
                <button @click="clearValue()">AC</button>
            </div>
        </div>
        <div class="equalArea">
            <button @click="calculationProcess()">=</button>
        </div>
    </div>
</template>

<style scoped>
.mainView{
    grid-area: views;
}

.buttonTop{
    grid-area: tops;
    display:grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
}

.buttonBottom{
    grid-area: bottoms;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr 1fr;
}

.equalArea{
    grid-area:equals;
}


.container{
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: 100px repeat(6, 70px) ;
    grid-template-areas:
        "views views views views"
        "tops tops tops tops"
        "bottoms bottoms bottoms equals"
        "bottoms bottoms bottoms equals"
        "bottoms bottoms bottoms equals"
        "bottoms bottoms bottoms equals"
        "bottoms bottoms bottoms equals";
    gap: 10px;
    background-color: #2196F3;
    padding: 10px;
}

.container > div {
  background-color: rgba(255, 255, 255, 0.8);
  text-align: center;
  padding: 20px 0;
  font-size: 30px;
}


</style>