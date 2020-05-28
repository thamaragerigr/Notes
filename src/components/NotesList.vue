<template>
  <div class="NotesList">
      <button class="NotesList-createButton" @click="createNote">New note</button>
     <nav>
         <p v-if="!notes.length">No notes saved</p>
         <ul class="NotesList-list" v-if="notes.length">
             <li 
                v-for="note in notes" 
                :key="note.title"
                @click="currentNote = note"
                :class="{ active : note === currentNote }">    
                <button>
                    {{ note.title }}
                </button>
            </li>
         </ul>
     </nav>
     <div v-if="currentNote">
         <button @click="deleteNote" class="NotesList-createButton">trash</button>
         <input type="text" v-model="currentNote.title" ref="noteTitle">
         <textarea v-model="currentNote.content" cols="30" rows="10"></textarea>
     </div>
  </div>
</template>

<script>
export default {
  name: 'NotesList',
  data() {
     return {
        notes: [],
        currentNote: null
     }
  },
  methods: {
      createNote(){
          const newNote = 
          {
              title: '',
              content: ''
          };
          this.notes.push(newNote);
          this.currentNote = newNote;
          this.$nextTick(function(){
              this.$refs.noteTitle.focus();
          })
      },
      deleteNote(){
              const index = this.notes.indexOf(this.currentNote)
              if (index !== -1) {
                 this.notes.splice(index, 1)
                 this.currentNote = null
              }
        }
  },
  mounted() {
      if(localStorage.notes) {
          this.notes = JSON.parse(localStorage.notes);
      }
  },
  watch: {
      notes: {
          handler(newNote){
          localStorage.notes = JSON.stringify(newNote);
      },
      deep: true
    }
  }
}
</script>

<style>
.NotesList{
    background: linear-gradient(180deg, rgba(48, 68, 78, 0.5) 63.02%, rgba(48, 68, 78, 0) 100%);
    box-shadow: 0px 1px 14px #19282F;
    border-radius: 100px 100px 0px 0px;
    /* height: 100vh; */
}

.active{
    background: rgba(48, 68, 78, 0.7);
    /* border-bottom: 1px solid rgba(184, 194, 192, .35); */
}

.NotesList-createButton{
    color: white;
    background: #3DD598;
    border: none;
    padding: 10px 15px;
    border-radius: 5px;
    font-weight: 700;
    font-size: 20px;
    margin-top: 40px;
    font-family: 'Quicksand', sans-serif;
    cursor: pointer;
}

.NotesList-list{
    text-align: left;
    list-style: none;
    padding: 0;
}

li{
    border-bottom: 1px solid rgba(184, 194, 192, .35);
    margin: 0px 50px;
    padding: 15px 5px;
    cursor: pointer;
    transition: .3s;
}

li button{
  background: none;
  border: none;
  color: white;
  font-size: 20px;
  font-weight: lighter;
  font-family: 'Quicksand', sans-serif;
}

input{
    background: rgba(48, 68, 78, 0.7);
    box-shadow: 0px 1px 14px #19282F;
    border-radius: 5px;
    border:none;
    color: white;
    font-family: 'Quicksand', sans-serif;
    padding: 10px 25px;
    margin: 10px;
    font-size: 20px;
    font-weight: lighter;
}

textarea{
    background: rgba(48, 68, 78, 0.7);
    box-shadow: 0px 1px 14px #19282F;
    border-radius: 5px;
    border:none;
    color: white;
    font-family: 'Quicksand', sans-serif;
    padding: 10px 25px;
    margin: 10px;
    font-size: 20px;
    font-weight: lighter;
}
</style>