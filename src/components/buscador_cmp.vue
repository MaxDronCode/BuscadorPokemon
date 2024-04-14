<template>
    <form @submit.prevent="conectaAPI">
        <input v-model="message" type="text" class="inputText">
        <input type="submit" value="Buscar" class="css-button-rounded--black">
    </form>
</template>

<script>
export default {
  name: 'buscador_cmp',
  data() {
    return {
        message: "",
    }
  },
  methods: {
    conectaAPI(){
        this.$emit('conectaAPI', this.message)
    }
  } 
  
}
</script>

<style scoped>
form{
  box-sizing: content-box;
  /* border: 1px solid black; */
  width: 420px; 
  margin: auto;
}
.inputText{
  box-sizing: content-box;
  width: 400px;
  height: 50px;
  border-radius: 8px;
  outline: none;
  font-size: 30px;
  text-align: center;
  
}
.inputText:focus{
  box-shadow: 0 0 3px 3px #6c7388;
}
.css-button-rounded--black {
  min-width: 130px;
  height: 40px;
  color: #fff;
  padding: 5px 10px;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  display: inline-block;
  outline: none;
  border-radius: 5px;
  border: 2px solid #212529;
  background: #212529;
  margin-top: 10px;
}
.css-button-rounded--black:hover {
  background: #fff;
  color: #212529
}
</style>