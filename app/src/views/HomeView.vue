<script setup>
import { onMounted, ref, computed } from 'vue'
import { supabase } from '@/supabase'
import Cards from '../components/Cards.vue'

const pokemons = ref([])

async function getPokemon() {
  const { data } = await supabase.from('pokedex').select('*')
  pokemons.value = data
  console.log(pokemons.value)
}


const selectedType = ref(null); 
const filteredPokemons = computed(() => {
  if (!selectedType.value) return pokemons.value;
  return pokemons.value.filter(pokemon => 
    pokemon.type1 === selectedType.value || pokemon.type2 === selectedType.value
  );
});

function filterByType(type) {
  selectedType.value = type;
}


const isFire = ref(false)
function yesfire(){
  isFire.value != isFire.value
}

onMounted(()=>{
  getPokemon()
})

</script>

<template>

<button @click="filterByType(null)">Show All</button>
<button @click="filterByType('Fire')">Fire</button>
<button @click="filterByType('Water')">Water</button>
<button @click="filterByType('Grass')">Grass</button>


<Cards v-for="pokemon in filteredPokemons" :name="pokemon.name" :type1="pokemon.type1" :type2="pokemon.type2" :hp="pokemon.hp"/>


</template>
