<script setup>
import { computed , ref } from "vue";
import { productos } from "./datos";

const index = ref(1); 

const getImage = computed(() => {
  const name = productos[index.value - 1].nombre.toLowerCase();
  return `https://www.html6.es/img/rey_${name}.png`;
});

const getName = computed(() => { 
  const name=productos[index.value - 1].nombre;
  return name[0].toUpperCase() + name.slice(1).toLowerCase();
});

const getPrice = computed(() => {  
  return ((productos[index.value - 1].precio)*0.9).toFixed(2);
});
 
const next =()=>{
  index.value++;
  if(index.value>7)index.value=1;
} 
</script>

<template>
  <main>
    <h1>Cena {{ index }} con el rey godo  <span class="name">{{ getName }}</span></h1>
    <br />
    <h3>Precio <span class="price">S/{{  productos[index - 1].precio }}</span></h3>
    <span v-if="productos[index-1].finDeSemana" class="weekend-free">
      (Solo fines de semana)
    </span>
    <span v-else class="weekend-busy">
      (De lunes a domingo)
    </span>
     <br><br>
    <div v-show="!productos[index-1].finDeSemana" class="discount">
      <span>Ahora un 10% dto: S/{{ getPrice }}</span>
      <img class="tag" src="/oferta.jpg" alt="tag">
    </div>
    <br/> 
    <img class="avatar" :src="getImage" alt="king" />
    <br />
    <button @click="next" >Siguiente ({{ index }}/{{ productos.length }})</button>
  </main>
</template>

<style scoped>
main {
  width: calc(100%-8px);
  margin: 8px;
  min-height: calc(100vh - 19px);
  border: 2px solid black;
  border-radius: 16px;
  text-align: center;
}

.name{
  text-transform: capitalize;
  color: blue;
}

.avatar{
  margin: 24px 0px;
}

.price{
  font-size: larger;
  color: blue;
}

.weekend-busy{
  background-color: green;
  color: white;
  padding:4px 16px;
  border-radius: 16px;
}

.weekend-free{
  background-color: red;
  color: white;
  padding:4px 16px;
  border-radius: 16px;
}

.tag{
  width: 50px;
  padding: 0px 8px;
}

.discount{
  display: flex;
  justify-content: center;
  align-items: center;
}

</style>
