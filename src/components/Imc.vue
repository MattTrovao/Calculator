<template>
  <p class="name">
    <span>IMC</span>
  </p>

  <div class="fields">
    <fieldset class="fields__group">
      <label for="size">Altura</label>

      <input type="number" name="size" id="size" min="0" step="10" v-model="size" placeholder="1,80">
    </fieldset>

    <fieldset class="fields__group">
      <label for="height">Peso</label>

      <input type="number" name="height" id="height" min="0" step="10" v-model="height" placeholder="80">
    </fieldset>

    <button 
      type="submit" 
      class="btn green small"
      @click="getImcValue"
      :disabled="!height && !size"
    >
      Calcular
    </button>
  </div>

  <p class="value" v-if="imcValue">
    {{imcValue.toFixed(2)}}
    <span>
      <template v-if="imcValue.toFixed(2) < 18.5">Abaixo do Peso</template>
      <template v-if="imcValue.toFixed(2) > 18.5 && imcValue.toFixed(2) < 24.9">Peso normal</template>
      <template v-if="imcValue.toFixed(2) > 25 && imcValue.toFixed(2) < 29.9">Sobrepeso</template>
      <template v-if="imcValue.toFixed(2) > 30 && imcValue.toFixed(2) < 34.9">Obesidade grau 1</template>
      <template v-if="imcValue.toFixed(2) > 35 && imcValue.toFixed(2) < 39.9">Obesidade grau 2</template>
      <template v-if="imcValue.toFixed(2) >= 40">Obesidade grau 3</template>
    </span>
  </p>

  <div class="calc">
    <p>
      Formula utilizada: <br>
      <b>Peso / (Altura^2)</b>
    </p>
  </div>
</template>

<script setup>
import { ref } from "vue";

const height = ref();
const size = ref();

const imcValue = ref(null)

const getImcValue = () => {
  imcValue.value = height.value / (size.value**2)
}
</script>