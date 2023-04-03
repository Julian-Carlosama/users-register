<template>
  <!-- This  main container -->
  <div class="flex flex-col p-4 pt-18 h-full">
    <h1 class="text-center justify-center text-4xl font-mono pt-20 font-bold mb-20 text-gray-800">Registro de Usuario</h1>
    <!-- This is progress line container -->
    <div class="max-w-md mx-auto mb-20">
      <LineLife></LineLife>
    </div>
    <!--FormStructure></FormStructure-->
    <FormStruct></FormStruct>
  </div>
</template>

<script>
import LineLife from './components/LineLife.vue'
//import FormStructure from './components/FormStructure.vue'
import FormStruct from './components/FormStruct.vue'

export default {
  name: 'App',
  components: {
    LineLife,
    //FormStructure,
    FormStruct
  },
  /*data() {
  return {
    steps: [
    'Paso 1', 'Paso 2', 'Paso 3'
    ],
    currentStep: 1,
  };
},*/
}
</script>
