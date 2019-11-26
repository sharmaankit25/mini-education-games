<template>
<div class="q-pa-sm">
  <span class="text-h6" v-if="num" padding>{{ num }}</span>
  <q-input v-else label="Enter Number" />
</div>
</template>
<script>
export default {
  props:['num']
}
</script>
