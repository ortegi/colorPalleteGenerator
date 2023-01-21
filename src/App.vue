
<script setup>
  import {ref, onMounted} from 'vue'
  import ColorShow from './componentss/ColorShow.vue'

 const digits = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F']
 const colorData = ref([])

 const generateHex = () =>{
  let hexColor = ''
  for (let i = 0; i < 6; i++){  
    const num = Math.floor(Math.random() * digits.length)
    hexColor += digits[num]
  }
  return hexColor
  }

onMounted( () =>{
  window.addEventListener("keypress", e => {
		if(e.code === 'Space' || e.code === 'Enter'){
      fetchData()
    
    }
   
	});

})

const fetchData = async () =>{
  const hexColor= generateHex()
  try{
    const res = await fetch(`https://www.thecolorapi.com/scheme?hex=${hexColor}&mode=analogic`)
    const jsonResponse = await res.json()
    colorData.value = jsonResponse.colors
    console.log(colorData.value)
  }catch(error){
    console.log(error)
  }
}

fetchData()
</script>

<template>
  <div class="container">
    <div class="row">
      <h1 class="text-center mt-5 mb-5"> Color pallete generator</h1>
    </div>
    
    <div class="row">

      <ColorShow 
      v-for="colors in colorData"
      :color="colors.hex.value"
      :name="colors.name.value"
      class="mx-auto"
      />
    </div>

    <div class="row">
      <button class="btn btn-primary mt-5 gene-btn" @click="fetchData()">  Generate Pallete</button>
      <p class="text-center mt-2"> Or just press the "SpaceBar" or "Enter" to generate new Palletes </p>
    </div>
  
  </div>
</template>

<style scoped>
.gene-btn{
  width: 400px;
  padding: 12px;
  margin: 0 auto;
  font-size: 18px;
}
</style>