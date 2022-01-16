<template>
 <div class="conversor">
     <h2>USD para BRL</h2>
     <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaA">
     <input type="button" value="Converter" v-on:click ="convertendo_USDBRL">
     <h1 id="resp">{{this.moedaB_value}}</h1>
 </div>
  <div class="conversor">
     <h2>BRL para USD</h2>
     <input type="text" v-model="moedaA2_value" v-bind:placeholder="moedaA">
     <input type="button" value="Para BRL" v-on:click ="BRLUSD">
     <h1 id="resp">{{this.moedaB2_value}}</h1>
 </div>

    
</template>

<script>
    let moedas = ["USD","BRL","JPN","EUR"];
    alert(moedas)
    export default {
        

        name: "conversor",
        data(){
            return{
                moedaA_value : "",
                moedaA2_value : "",
                moedaB_value : "-",
                moedaB2_value : "*"
            }
        },
        methods:
        {
            convertendo_USDBRL(){
            
                let de_para = moedas[0]+"-"+moedas[1];
                let url = "https://economia.awesomeapi.com.br/last/"+de_para;
                fetch(url).then(res=>{return res.json()})
                          .then(json=>
                          {
                              let cotacao = json[moedas[0]+moedas[1]];
                              this.moedaB_value = "R$ "+parseFloat(cotacao["high"] *(this.moedaA_value)).toFixed(2);
                              
                              
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
            }
        
        
        }
        
    }
    
</script>

<style scoped>
.conversor
{
    
    background-color: lightsteelblue;
    width: 200px;
    margin: 25px;
    display: inline-table;
}
#resp
{
    color: greenyellow;
    font-size: 30px;
}

</style>
