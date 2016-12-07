<template>
  <input type="text" :value="value" @input="update($event)" />
</template>

<script>
import Cleave from 'cleave.js'

export default {
  props: {
    value: '',
    options: {
      type: Object,
      default: () => ({})
    }
  },

  data () {
    return {
      cleave: null
    }
  },

  mounted () {
    this.$nextTick(() => {
      this.cleave = new Cleave(this.$el, this.options)
    })
  },

  beforeDestroy () {
    this.cleave.destroy()
  },
  
  methods: {
    update ($event) {
      
      // fixes the bug with extra chars at the end
      setTimeout(() => {
        this.$emit('input', this.cleave.getFormattedValue())
      }, 10);
    }
  },
  
}
</script>
