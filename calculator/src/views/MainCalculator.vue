<script setup>
import { ref } from 'vue'

const inputA = ref('')
const inputB = ref('')
const inputArr = ref([])
const initial = ref(true)

const sumNum = ()=>{
    if (initial.value){
        initial.value = false
        inputB.value = String(Number(inputA.value) + Number(inputB.value))
    } else{
        initial.value = true
        inputA.value = (Number(inputA.value) + Number(inputB.value))
    }
    
}


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
    console.log(char)
    // const keys = ['+','-','x','/']
    // if (inputArr.value.length % 2 == 0 && keys.includes(char)){
    //     input.value = "Input Invalid"
    // } else if (inputArr.value.length % 2 != 0 && !isNaN(Number(char))){
    //     input.value = "Input Invalid"
    // } else if (char == '.'){
    //     if (isNaN(Number(inputArr.value[inputArr.value.length-1]))){
    //         input.value = "Input Invalid"
    //     } else{
    //         input.value += char
    //         inputArr.value[inputArr.value.length-1] += char
    //     }
    // }
    //  else{
    //     input.value += char
    //     inputArr.value.push(char)
    // }

    if (initial.value){
        inputA.value += char
    } else{
        inputB.value += char
    }
    
    console.log(inputArr.value)
    
}

function clearValue(){
    inputArr.value=[]
    input.value = ''
}
</script>

<template>
    <div class="container">
        <div v-if="initial" class="mainView">{{ inputA ? inputA: 0 }}</div>
        <div v-else class="mainView">{{ inputB ? inputB: 0 }}</div>
        <div class="buttonTop">
            <div>
                <button class="top-row" @click="sumNum()">+</button>
            </div>
            <div>
                <button class="top-row" @click="addSymbol('-')">-</button>
            </div>
            <div>
                <button class="top-row" @click="addSymbol('x')">x</button>
            </div>
            <div>
                <button class="top-row" @click="addSymbol('/')">/</button>
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
                <button class="left-bottom-corner" @click="addSymbol('0')">0</button>
            </div>
            <div>
                <button @click="addSymbol('.')">.</button>
            </div>
            <div>
                <button  @click="clearValue()">AC</button>
            </div>
        </div>
        <div class="equalArea">
            <button class="equal-button" @click="calculationProcess()">=</button>
        </div>
    </div>
</template>

<style scoped>
*{
    font-family: sans-serif;
}
.mainView{
    grid-area: views;
    background-color: black;
    color:white;
    padding: 20px 20px 20px 0;
    font-size: 50px;
    text-align:right;
    border-radius: 30px 30px 0 0;
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
    border-radius: 0 0 30px 0;
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
    
    background-color: aqua;
    padding: 10px;
    border-radius: 20px;
}
button {
    border: 0.2px solid #5a5a5a;
    background-color:azure;
    text-align: center;
    text-decoration: none;
    font-size: 20px;
    width:100%;
    height:100%;
    display:block;
}

.equal-button{
    background-color:firebrick;
    border-radius:0 0 30px 0;
}

.left-bottom-corner{
    border-radius:0 0 0 30px;
}

.top-row{
    background-color:rgba(171, 171, 171, 0.806);
}

/* .container > div {
  background-color: rgba(255, 255, 255, 0.8);
  text-align: center;
  
} */


</style>