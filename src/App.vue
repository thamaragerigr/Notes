<template>
  <div id="app">
    <div>
      <div class="dots">
        <span class="yellow"></span>
        <span class="red"></span>
        <span class="green"></span>
      </div>
      <h1>Notes</h1>
    </div>
    <NotesList/>
  </div>
</template>

<script>
import NotesList from './components/NotesList.vue'

export default {
  name: 'App',
  components: {
    NotesList
  }
}
</script>

<style>
body {
  background: #22343C;
  color: white;
  font-family: 'Quicksand', sans-serif;
  text-align: center;
}

#app{
  margin: auto;
  max-width: 375px;
  min-height: 665px;
  padding: 10px;
  border: 1px red solid;
}

.dots{
  display: flex;
  justify-content: center;
}
.yellow{
  margin: 5px;
  width: 15px;
  height: 10px;
  background: #FFC542;
  border-radius: 6px;
}
.red{
  margin: 5px;
  width: 15px;
  height: 10px;
  background: #FF575F;
  border-radius: 6px;
}
.green{
  margin: 5px;
  width: 15px;
  height: 10px;
  background: #3DD598;
  border-radius: 6px;
}
h1{
  margin: 0;
}
</style>
