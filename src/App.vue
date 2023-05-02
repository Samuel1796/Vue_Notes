<script setup>
import { ref } from 'vue';

const showModal = ref(false);
const newNote = ref("");
const notes = ref([]);
const errorMessage = ref("");

const getRandomColor = ()=>{
  let color = "hsl("+Math.random()*360 +", 100%, 75%)";
  return color;
}

const addNote = ()=>{
  if(newNote.value.length<9){
    errorMessage.value = "Note too short. It should be more than nine words"
}else{
  notes.value.push({
    id: Math.floor(Math.random()*1000000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor()
  })
  showModal.value=false;
  newNote.value="";
  errorMessage.value = "";
}
}
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
        <div class="modal">
          <textarea v-model.trim="newNote" name="notes" id="notes" cols="30" rows="10"></textarea>
          <p v-if="errorMessage">{{errorMessage}}</p>
          <button @click="addNote">Add Note</button>
          <button class="close" @click="showModal=false" >Close</button>
        </div>
    </div>



    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" :key="note.id" class="card" :style="{backgroundColor: note.backgroundColor}">
          <p class="main-text">{{note.text}}</p>
          <p class="date">{{note.date }}</p>
        </div>
      </div>
      
      
    </div>
  </main>
</template>

<style scoped>
  main{
    height: 100vh;
    width: 100vw;

  }
  .container{
    max-width: 1000px;
    padding:10px ;
    margin: 0 auto;

  }
  header{
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  h1{
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }
  .cards-container{
    display: flex;
    flex-wrap: wrap;
  }
 header button{
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(21,20,20);
    border-radius: 100%;
    color: white;
    font-size: 20px;
  }
  .card{
    width: 240px;
    height: 240px;
    background-color: rgb(237,182,44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
  }
  .overlay{
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0,0,0.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .date{
    font-size: 12.5px;
    font-weight: bold;
  }
  .modal{
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }
  .modal button{
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;

  }
  .modal .close{
    background-color: red;
    margin-top: 7px;
  }
  .modal p{
    color:red ;
  }

</style>