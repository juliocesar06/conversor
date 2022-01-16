<template>
  <div id='ini'>
    <h1 id='title'>CONVERSOR MOEDA</h1>
    <conversor/>
  </div>
</template>

<script>
import Conversor from './components/Conversor.vue'

export default {
  name: 'App',
  components: {
    Conversor
  }
}
</script>

<style>
#ini
{
  background-image:url("https://s.yimg.com/ny/api/res/1.2/KCnIKG6qegEzI9uYSv0rJA--/YXBwaWQ9aGlnaGxhbmRlcjt3PTY0MDtoPTQyNw--/https://s.yimg.com/os/creatr-uploaded-images/2021-10/fc417280-31d7-11ec-bfff-6f1dc2c1f045");
  
  position: absolute;
  top: 0;  
  left: 0;
  height: 610px;

}
#title
{
  color: black;
  font-size: 40px;
  margin-bottom: -5px;
  margin-top: 5px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
