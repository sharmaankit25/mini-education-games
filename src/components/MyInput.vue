<template>
<div class="q-pa-sm">
  <span class="text-h6" v-if="num != null" padding>{{ num }}</span>
  <q-input v-else label="Enter Number" :value="dueDate"
    @input="$emit('update:dueDate', $event)" />
</div>
</template>
<script>
export default {
  props:['num']
}
</script>
