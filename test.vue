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
                this.dollars = this.reals / this.currentQuotation;
            } else {
                this.dollars = '';
            }
        },
        dollars: function() {
            if (!Number.isNaN(this.dollars)) {
                this.reals = this.dollars * this.currentQuotation;
            } else {
                this.reals = '';
            }
        }
    }
}
</script>