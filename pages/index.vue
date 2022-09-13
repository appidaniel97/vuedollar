<template class="style-none">
    <body class="gradient">
    <div class="formMod">
            <img src="onedollar.png"/>
            <h2>Dolares</h2>
            <input type="text" v-model="dollars" />
            <h2>Vale</h2>
            <input type="text" v-model="reals" />
            <h2>Reais</h2>   
    </div>      
    </body>   
</template>

<script>
import axios from 'axios';

export default {
    async asyncData(){
        const api = 'https://economia.awesomeapi.com.br/last/USD-BRL';
        const { USDBRL: data } = await axios.get(api).then((response) => {
            return response.data;
        }).catch((err) => {
            console.error(err);
        });

        let { bid: currentQuotation } = data;
        currentQuotation = Number.parseFloat(currentQuotation).toFixed(2);

        return {
            dollars: Number.parseFloat(1.00).toFixed(2),
            currentQuotation: currentQuotation,
            reals: Number.parseFloat(currentQuotation * 1.00).toFixed(2)
        }
    },

    watch: {
        reals: function() {
            if (!Number.isNaN(this.reals)) {
                this.dollars = Number.parseFloat(this.reals / this.currentQuotation).toFixed(2);
            } else {
                this.dollars = '';
            }
        },
        dollars: function() {
            if (!Number.isNaN(this.dollars)) {
                this.reals = Number.parseFloat(this.dollars * this.currentQuotation).toFixed(2);
            } else {
                this.reals = '';
            }
        }
    }
}
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