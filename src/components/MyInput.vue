<template>
<div class="q-pa-sm">
  <span class="text-h6" v-if="num != null" padding>{{ num }}</span>
  <q-input v-else label="Enter Number"
    outlined
    :value="num"
    autofocus
    @input="$emit('update:num', $event)" />
</div>
</template>
<script>
export default {
  props:['num']
}
</script>
