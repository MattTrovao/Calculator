<template>
  <p class="name">
    <span>Valor Hora</span>
  </p>

  <div class="fields">
    <fieldset class="fields__group">
      <label for="hours">Total de Horas (por semana)</label>

      <select id="hours" v-model="workHours">
        <option value="44">44 Horas (8h)</option>
        <option value="36">36 Horas (6h)</option>
        <option value="20">20 Horas (4h)</option>
      </select>
    </fieldset>

    <fieldset class="fields__group">
      <label for="wage">Salário</label>

      <input
        type="number"
        name="wage"
        id="wage"
        min="0"
        step="100"
        v-model="totalWage"
        placeholder="1200"
      />
    </fieldset>

    <button 
      type="submit" 
      class="btn green small"
      @click="getHourValue"
      :disabled="!totalWage"
    >
      Calcular
    </button>
  </div>

  <p class="value" v-if="hourValue">
    <span>R$</span>
    {{hourValue.toFixed(2)}}
  </p>

  <div class="calc">
    <p>
      Formula utilizada: <br>
      <b>Salário / [ (Horas Trabalhadas / 6) * 30 ]</b>
    </p>
  </div>
</template>

<script setup>
import { ref } from "vue";

const workHours = ref(44);
const totalWage = ref();

const hourValue = ref(null)

const getHourValue = () => {
  hourValue.value = totalWage.value / ( (workHours.value / 6) * 30 )
}
</script>
