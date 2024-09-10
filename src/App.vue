<template>
  <div style="display:flex;flex-direction: row;">
    <DrumInput :values="[
      'jan', 'feb', 'mar', 'apr', 'may', 'jun', 'jul', 'aug', 'sep', 'oct', 'nov', 'dec'
    ]" v-model:value="mon" />
    <DrumInput :values="[
      '01', '02', '03', '04', '05', '06', '07',
      '08', '09', '10', '11', '12', '13', '14',
      '15', '16', '17', '18', '19', '20', '21',
      '22', '23', '24', '25', '26', '27', '28',
      '29', '30', '31',
    ]" v-model:value="date"/>
    <DrumInput :values="[
      '2022', '2023', '2024', '2025'
    ]" v-model:value="year"/>
  </div>
  select = {{ mon }} {{ date }} {{ year }}
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import DrumInput from './components/DrumInput.vue';

export default defineComponent({
  name: 'App',
  components: {
    DrumInput
  },
  setup() {
    const mon = ref('jan');
    const year = ref('2024');
    const date = ref('01');
    return {
      mon, year, date,
    }
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
