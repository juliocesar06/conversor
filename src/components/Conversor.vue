<!--
template cada componente esta nessa div
-->
<template >
<div id='principal'>
    <!--div converte usd brl-->
    <div class="conversor bra">
        <h2>USD para BRL</h2>
        <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaA">
        <input type="button" value="para BRL" v-on:click ="convertendo_USDBRL">
        <h1 class="resp-br">{{this.moedaB_value}}</h1>
    </div>
    <!--div converte  brl usd-->
    <div class="conversor usa">
        <h2>BRL para USD</h2>
        <input type="text" v-model="moedaA2_value" v-bind:placeholder="moedaA">
        <input type="button" value="Para USD" v-on:click ="BRLUSD">
        <h1 id="resp">{{this.moedaB2_value}}</h1>
    </div>
    <!--div converte  brl uer-->
    <div class="conversor eur">
        <h2>BRL para EUR</h2>
        <input type="text" v-model="moedaA4_value" v-bind:placeholder="moedaA">
        <input type="button" value="Para EUR" v-on:click ="BRLEUR">
        <h1 id="resp">{{this.moedaB4_value}}</h1>
    </div>
    <!--div converte uer brl-->
    <div class="conversor bra">
        <h2>EUR para BRL</h2>
        <input type="text" v-model="moedaA3_value" v-bind:placeholder="moedaA">
        <input type="button" value="Para BRL" v-on:click ="EURBRL">
        <h1 class="resp-br">{{this.moedaB3_value}}</h1>
    </div>
</div>
    
</template>

<!--scrips js

toda a logica de programaçao esta nesse parte
-->
<script>
    // lista com as siglas das moedas
    let moedas = ["USD","BRL","JPN","EUR"];
    // exportando 
    export default {
        

        name: "conversor",
        data(){
            return{
                //variaveis que estao em uso no programa para retorno e receber dados
                //recebe [set]
                moedaA_value : "",
                moedaA2_value : "",
                moedaA3_value : "",
                moedaA4_value : "",
                // mostra [get]
                moedaB_value : "-",
                moedaB2_value : "-",
                moedaB3_value : "-",
                moedaB4_value : "-",
            }
        },
        //funçoes que o programa possue
        methods:
        {

            convertendo_USDBRL(){
                
                //recebe 2 string da lista moedas e une as 2 string com - no meio completando o request na api
                let de_para = moedas[0]+"-"+moedas[1];
                //url é caminho para consumir a api
                let url = "https://economia.awesomeapi.com.br/last/"+de_para;
                //resposta dado pelo servidor da api apos then(entao) 
                //fecth == resposta
                //then == o que ira fazer com essa resposta
                fetch(url).then(res=>{return res.json()})//retornando uma resposta em json
                          .then(json=>
                          {
                              // a api exige um parametro para acesso como ex: BRLUSD 
                              // cotaçao recebe esse parametro e acessa usando a combinaçao de string da lista moedas
                              let cotacao = json[moedas[0]+moedas[1]];
                              ///a resultado que quero nessa parte é a conversao da moeda
                              //como cotaçao pega o valor da moeda eu faço a operaçao nescessario usando a definiçao da cotaçao["high"]
                              //cotaçao[high] = é um parametro jsn da especifica da api
                              this.moedaB_value = "R$ "+parseFloat(cotacao["high"] *(this.moedaA_value)).toFixed(2);
                              
                              //OBS TODA API TEM QUE SER LIDA POIS CADA UMA TEM PARTICULIDADES DIFERENTES.
                          }
                          ) 
            },
             BRLUSD(){
            
                let de_para = moedas[0]+"-"+moedas[1];
                let url = "https://economia.awesomeapi.com.br/last/"+de_para;
                fetch(url).then(res=>{return res.json()})
                          .then(json=>
                          {
                              let cotacao2 = json[moedas[0]+moedas[1]];
                              this.moedaB2_value = "$ "+ parseFloat(this.moedaA2_value / cotacao2["high"]).toFixed(2);
                              
                              
                          }
                          ) 
            },
            EURBRL(){
            
                let de_para = moedas[1]+"-"+moedas[3];
                let url = "https://economia.awesomeapi.com.br/last/"+de_para;
                fetch(url).then(res=>{return res.json()})
                          .then(json=>
                          {
                              let cotacao3 = json[moedas[1]+moedas[3]];
                              this.moedaB3_value = "R$ "+ parseFloat(this.moedaA3_value / cotacao3["high"]).toFixed(2);
                              
                              
                          }
                          ) 
            },
            BRLEUR(){
            
                let de_para = moedas[1]+"-"+moedas[3];
                let url = "https://economia.awesomeapi.com.br/last/"+de_para;
                fetch(url).then(res=>{return res.json()})
                          .then(json=>
                          {
                              let cotacao4 = json[moedas[1]+moedas[3]];
                              this.moedaB4_value = "€ "+ parseFloat(this.moedaA4_value * cotacao4["high"]).toFixed(2);
                              
                              
                          }
                          ) 
            }
        
        
        }
        
    }
    
</script>

<style scoped>

#principal{
   
    padding: 10px;
    background-image:  url("https://i.pinimg.com/736x/a5/4e/b5/a54eb512e607f9d7ddd2c445b29ccdfd.jpg");
    border-radius: 50px;
    
}

h2
{
    color: black;
}
.conversor
{
    border-radius: 50px;
    background-image: url("https://www.infomoney.com.br/wp-content/uploads/2019/06/estados-unidos-eua.jpg?fit=900%2C554&quality=50&strip=all");
    width: 500px;
    margin: 25px;
    display: inline-table;
    
}
.conversor.eur
{
    border-radius: 50px;
    background-image: url("img/bandeira-da-europa.jpg");
    background-size: 500px 500px;
    width: 500px;
    margin: 25px;
    display: inline-table;
    
}
.conversor.bra
{
    border-radius: 50px;
    background-image: url("https://www.jornalcontabil.com.br/wp-content/uploads/2016/10/bandeira-do-brasil.jpg");
    background-size: 500px 500px;
    width: 500px;
    margin: 25px;
    display: inline-table;
    
}
#resp
{
    color: greenyellow;
    font-size: 50px;
}
.resp-br
{
    color: black;
    font-size: 50px;
}

</style>
