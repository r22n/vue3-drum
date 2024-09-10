<template>
  <div class="drumbody" ref="body" @scroll="scroll">
    <div>
      <p> </p>
    </div>
    <div :key="`i-${i}`" :id="`i=${i}`" :class="e !== model && 'whiteout'" v-for="e, i in values">
      <p>{{ e }}</p>
    </div>
    <div>
      <p> </p>
    </div>
  </div>
</template>

<style scoped>
.drumbody {
  overflow-y: scroll;
  height: 80px;
  font-weight: bold;
  white-space: pre;
  display: flex;
  flex: 1 1 auto;
  flex-direction: column;
  user-select: none;
}

.whiteout {
  color: lightgray;
}
</style>

<script setup lang="ts">
import { defineProps, defineModel, ref, watch, onMounted } from 'vue';

const model = defineModel('value', {
  default: ''
});
watch(model, e => {
  if (mset) {
    mset = 0;
    return;
  }
  const { d, el, m } = vpos();
  const i = props.values.indexOf(e);
  el.scrollTop = d * i + m / 2;
});
onMounted(() => {
  const { d, el, m } = vpos();
  const i = props.values.indexOf(model.value);
  el.scrollTop = d * i + m / 2;
});
let mset = 0;


export type P = {
  values: string[];
}
const props = defineProps<P>();


const body = ref<HTMLDivElement>();
function scroll() {
  const { y, d } = vpos();
  const i = Math.floor(y / d);
  mset++;
  model.value = props.values[i - 1];
}


function vpos() {
  const el = body.value!;
  const h = el.scrollHeight;
  const m = el.clientHeight / 2;
  const y = el.scrollTop + m;
  const count = props.values.length + 1.8;
  const d = h / count;
  return {
    el,
    h, y,
    count,
    d, m
  };
}

</script>
