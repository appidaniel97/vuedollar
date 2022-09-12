<template class="style-none">
    <body class="gradient">
    <div class="formMod">
            <img src="onedollar.png"/>
            <h1>Dolar</h1>
            <input onClick="this.setSelectionRange(0, this.value.length)" onkeyup="handleGetQuotation(this.value)" type="text" id="dolar" value="1.00"/>
            <h3>Vale</h3>
            <input onClick="this.setSelectionRange(0, this.value.length)" onkeyup="handleGetDol(this.value)" type="text" id="reais"  />
            <h3>Reais</h3>        
            <h1>{{ titulo }}</h1>     
    </div>      
    </body>   
</template>



<script>
let senior;
let dolarDecimal;
import axios from 'axios';
//import Vue from 'Vue'

export default{
        async asyncData(){
        const api = 'http://economia.awesomeapi.com.br/last/USD-BRL'
        const getApi = await axios.get(api).then((response) =>{
            console.log(response)
             
            console.log(response.data,"TOMAAAAAAAAAAA")
            console.log(response.data.USDBRL['bid'],"RECEBAAAAAAAA")
            senior = response.data.USDBRL['bid']
            dolarDecimal = senior;
            console.log(dolarDecimal,"DOMMMMMMMMMMM")
            return response.data
        })
        return { getApi }
        
    },   
    
  data(){
    return{
        titulo: dolarDecimal
        
    }
  }
}
//export default {
//    async asyncData(){
//        const api = 'http://economia.awesomeapi.com.br/last/USD-BRL'
//        const getApi = await axios.get(api).then((response) =>{
//            console.log(response)
             
//            console.log(response.data,"TOMAAAAAAAAAAA")
//            console.log(response.data.USDBRL['bid'],"RECEBAAAAAAAA")
//            senior = response.data.USDBRL['bid']
//            dolarDecimal = senior;
//            return response.data
//        })
//        return { getApi }
//    },   
//    methods:{
//        md() {        
//            this.$refs.dan = 'Hello Bro';
//        }
//    }
//}


//new Vue({
//    el: '#formMod',
//    data: { 
//          message:"Welcome"
//      },
//      methods:{
//        handleGetQuotation:  this.$refs.reais.innerText = 'Hello Bro'
//    }
//});

//function cotacao(){
//    dolarDecimal = Number.parseFloat(senior).toFixed(2);
//    document.getElementById("reais").value = dolarDecimal;
//}


//function handleGetQuotation(value){
//    document.getElementById("reais").value = Number.parseFloat(value * dolarDecimal).toFixed(2);
//    console.log(value * dolarDecimal);
//}

//function handleGetDol(value){
//    document.getElementById("dolar").value = Number.parseFloat(value / dolarDecimal).toFixed(2);
//    console.log(value / dolarDecimal,"teste");
//    console.log(value, "reais")
//}

//cotacao()
</script>

<style>
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Poppins', sans-serif;
}

.gradient{
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    width: 100vw;
    background: linear-gradient(45deg, #084177, #687466, #6F8C6B, #fbc490) ;
    background-size: 300% 300%;
    animation: colors 5s ease infinite;
}

@keyframes colors{
    0% {
        background-position: 0% 50%;
    }
    50% {
        background-position: 100% 50%;
    }
    100% {
        background-position: 0% 50%;
    }
}

/*body{
    background-color: rgb(238, 234, 234);
}*/

.titleh1{
    color: rgb(223, 223, 223);
    align-items: center;
    justify-content: center;
    text-align: center;
    /*padding: 260px;*/
}

.symbol{
    display: inline-block;
    text-align: left;
    width: 2.1em;
    /*margin-left: 500px;*/
}


#estranger{
     font-size: 25px;
     text-align: center;
     margin-left: 600px;
     
}

#br{
    font-size: 25px;
    text-align: center;
    margin-left: 50px;
}

.formMod img{
    max-width: 300px;
    align-items: center;
    justify-content: center;
    display: flex;
    position: flex;
    padding: 0px;
}

.formMod h1{
    align-items: center;
    justify-content: center;
    text-align: center;
}

.formMod{
    padding-top: 20%;
    align-items: center;
    justify-content: center;
}

.formMod input{
    align-items: center;
    text-align: center;
    display: block;
    margin: 10px auto;
    max-width: 500px;
    width: 100%;
    height: 40px;
    border: 1px solid #430434;
    border-radius: 10px;
    font-size: 20px;
    border-color: green;;
}

.formMod h3{
    text-align: center;
    align-items: center;
    justify-content: center;
}

</style>