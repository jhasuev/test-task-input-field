<template>
  <div>
    <TextField
      v-model="text"
      class="text-field"
    />
  </div>
</template>

<script>
import TextField from './components/TextField.vue'

export default {
  name: 'App',
  components: {
    TextField,
  },
  data() {
    return {
      text: '',
    }
  },
}
</script>

<style>
.text-field {
  width: 100%;
  max-width: 326px;
  margin: auto;
}
</style>
