
<template>
  <main class="page">
    <section class="content">
      <div class="tab">
        <button 
          :class="`btn ${showVh ? 'active' : ''}`" 
          @click="changeCalculator('vH')">
          Valor Hora
        </button>
        <button 
          :class="`btn ${showFees ? 'active' : ''}`" 
          @click="changeCalculator('fees')">
          Juros
        </button>
        <button 
          :class="`btn ${showImc ? 'active' : ''}`" 
          @click="changeCalculator('imc')">
          IMC
        </button>
      </div>

      <div class="calculator">
        <Hour v-if="showVh"/>
        <Fees v-if="showFees"/>
        <Imc v-if="showImc"/>
      </div>
    </section>
  </main>
</template>

<script setup>
import { ref } from "vue";
import Fees from "./components/Fees.vue";
import Hour from "./components/Hour.vue";
import Imc from "./components/Imc.vue";

const showVh = ref(true);
const showFees = ref(false);
const showImc = ref(false);

const changeCalculator = (e) => {
  if (e == "vH") {
    showVh.value = true;
    showFees.value = false;
    showImc.value = false;
  }else if (e == 'fees') {
    showVh.value = false;
    showFees.value = true;
    showImc.value = false;
  }else {
    showVh.value = false;
    showFees.value = false;
    showImc.value = true;
  }
};
</script>

<style>
</style>
