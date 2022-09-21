<template class="style-none">
    <div class="div">
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta http-equiv="X-UA-Compatible" content="IE=edge">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <meta name="description" content="Cotação do dolar hoje. Veja a conversão de dolar para real e real para dolar">
            <meta name="keywords" content="DOLAR, REAL, COTAÇÃO, HOJE, CONVERSÃO">
            <meta name="author" content="Daniel Appi">
            <meta name="robots" content="index, follow">
            <link rel="canonical" href="http://realparadolar.com/">
            <title>Dolar Hoje</title>
        </head>
        <body class="gradient">
                <div class="formMod">
                    <img src="onedollar.png"/>
                    <h2>Dolares</h2>
                    <money onClick="this.setSelectionRange(0, this.value.length)" v-model="priceDollar" v-bind="moneyD"></money>
                    <h2>Vale</h2>
                    <money onClick="this.setSelectionRange(0, this.value.length)" v-model="priceReal" v-bind="moneyR"></money>
                    <h2>Reais</h2>   
                </div>      
            </body>   
            <footer>
                <cookie-law theme="dark-lime">
                    <div slot="message">
                        Utilizamos cookies essenciais e tecnologias semelhantes de acordo com a nossa <router-link to="politica-de-privacidade">Política de Privacidade</router-link> e, ao continuar navegando, você concorda com estas condições.
                    </div>
            </cookie-law>
            </footer>
        </html>
    </div>
    
</template>

<script async src="https://www.googletagmanager.com/gtag/js?id=G-ZFXFJ82F22"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());

gtag('config', 'G-ZFXFJ82F22');
</script>

<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-1771975771388751"
crossorigin="anonymous"></script>

<script>
import axios from 'axios';
import {Money} from 'v-money'
import CookieLaw from 'vue-cookie-law'


export default {
    components: {
        Money,
        CookieLaw
    }, 
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
            currentQuotation: currentQuotation,
            priceDollar: Number.parseFloat(1.00).toFixed(2),
            priceReal: Number.parseFloat(currentQuotation * 1.00).toFixed(2),
            
            moneyD: {
                decimal: ',',
                thousands: '.',
                prefix: 'US$ ',
                //suffix: ' #',
                precision: 2,
                masked: false
            },
            moneyR: {
                decimal: ',',
                thousands: '.',
                prefix: 'R$ ',
                //suffix: ' #',
                precision: 2,
                masked: false
            }            
        }
    },

    watch: {
        priceDollar: function() { 
            if (!Number.isNaN(this.priceDollar)) {
                this.priceReal = this.priceDollar * this.currentQuotation;//Number.parseFloat(this.priceDollar * this.currentQuotation).toFixed(2);
            } else {
                this.priceReal = '';
            }
        },
        priceReal: function() {
            if (!Number.isNaN(this.priceReal)) {
                this.priceDollar = this.priceReal / this.currentQuotation;//Number.parseFloat(this.priceReal / this.currentQuotation).toFixed(2);
            } else {
                this.priceDollar = '';
            }
        }
    },
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