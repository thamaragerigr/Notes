<template>
  <div class="Notes">
      <button @click="createNote">Create note</button>
     <nav>
         <p v-if="!notes.length">No notes saved</p>
         <ul v-if="notes.length">
             <li 
                v-for="note in notes" 
                :key="note.title">    
                <button 
                    :class="{ active : note === currentNote }"
                    @click="currentNote = note">
                    {{ note.title }}
                </button>
            </li>
         </ul>
     </nav>
     <div v-if="currentNote">
         <button @click="deleteNote">trash</button>
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
.active{
    background: red;
}
</style>