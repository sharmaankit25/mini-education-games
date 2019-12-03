<template>
<div class="q-pa-sm">
  <span class="text-h6" v-if="value != null" padding>{{ value }}</span>

</div>
</template>
<script>
export default {
  props:['value'],
  computed: {
    listeners() {
      return {
        ...this.$listeners,
        input:event => this.$emit('update:value',event)
      }
    }
  }
}
</script>
