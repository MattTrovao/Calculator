<template>
  <p class="name">
    <span>Juros</span>
  </p>

  <div class="fields">
    <fieldset class="fields__group">
      <label for="type">Tipo de Juros</label>


      <div class="radio">
        <input type="radio" name="typeFees" value="simple" v-model="typeFees" checked>
        <label for="typeFees">Juros Simples</label>
      </div>
      <div class="radio">
        <input type="radio" name="typeFees" value="compund" v-model="typeFees">
        <label for="typeFees">Juros Composto</label>
      </div>
    </fieldset>

    <fieldset class="fields__group">
      <label for="initial">Valor Inicial</label>

      <input
        type="number"
        name="initial"
        id="initial"
        min="0"
        step="100"
        v-model="initial"
        placeholder="1200"
      />
    </fieldset>

    <fieldset class="fields__group">
      <label for="tax">Taxa</label>

      <input
        type="number"
        name="tax"
        id="tax"
        min="0"
        v-model="tax"
        placeholder="1,5"
      />
    </fieldset>

    <fieldset class="fields__group">
      <label for="period">Período (meses)</label>

      <input
        type="number"
        name="period"
        id="period"
        min="0"
        v-model="period"
        placeholder="5"
      />
    </fieldset>

    <button 
      type="submit" 
      class="btn green small"
      @click="getFeesValue"
      :disabled="!initial && !tax && !period"
    >
      Calcular
    </button>
  </div>

  <p class="value" v-if="feesValue">
    {{feesValue.toFixed(2)}}
    <span>% (arredondado para cima)</span>
  </p>

  <div class="calc">
    <p>
      Formula utilizada (Juros Simples): <br>
      <b>(Valor Inicial x Taxa x Período) / 100</b>
    </p>

    <p>
      Formula utilizada (Juros Composto): <br>
      <b>(Valor Inicial x (1 + Taxa)^Período) / 100</b>
    </p>
  </div>
</template>

<script setup>
import { ref } from "vue";

const typeFees = ref()

const initial = ref()
const tax = ref()
const period = ref()

const feesValue = ref(null)

const getFeesValue = () => {
  if( typeFees.value == 'simple' ) {
    feesValue.value = (initial.value * tax.value * period.value) / 100
  } else {
    feesValue.value = (initial.value * (1 + tax.value)**period.value) / 100
  }
}
</script>
