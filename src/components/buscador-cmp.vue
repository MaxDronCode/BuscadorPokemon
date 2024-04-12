<template>
    <form @submit.prevent="conectaAPI">
        <input v-model="message" type="text">
        <input type="submit" value="Buscar">
    </form>
</template>

<script>
export default {
  name: 'buscador-cmp',
  data() {
    return {
        message:String
    }
  },
  methods: {
    conectaAPI(){
        this.$emit('conectaAPI', this.message)
    }
  }
  
}
</script>