<template>
 
 <user-profile :user="user" />
 
 <div class="container">
  <div class="row">
  
   <div class="col-lg-4 col-xs-12 offset-lg-4">
    
    <img alt="Vue logo" src="./assets/document_notebook.png">
    <hr>
    <small data-toggle="modal" data-target="#exampleModal" id="personalize">Personalized experience</small>
    <personalized v-on:getdata ="FetchData($event)" />
    <h2>Add your notes</h2>
    <button @click="RevealForm" type="button" class="btn btn-danger btn-circle btn-lg mb-3">+</button>
   
    <form @submit.prevent = "SumbitForm" v-bind:style = "{display: display }" >
      <div class="form-group">
      <input type="text" class="form-control"  placeholder="Enter title.." v-model="note.title">
      </div>
      <div class="form-group">
      <textarea type="text" class="form-control" rows = "3" placeholder="Enter description.." v-model="note.description"></textarea>
      </div>
      <button type="submit" class="btn btn-primary mb-3">Submit</button>
    </form>
    <div v-if="this.user.notes.length"> 
      
      <div class="card mb-3"  v-for="note in notesToShow" v-bind:key = note.id>
        
          <div class="card-body">
          <h5 class="card-title">{{note.title}}</h5>
          <h6 class="card-subtitle mb-2 text-muted">{{note.date}}</h6>
          <p class="card-text">{{note.description}}</p>
          <a @click="RemoveNote(note)" href="#" style="color:#08f26E" class="card-link">Done</a>
          <a href="#" class="card-link"></a>
          </div>
              
      </div>
    </div>
     <a v-if="this.user.notes.length" @click="IncreaseLimit" href="#" class="show-more mr-2">Show more</a>
     <a v-if="this.user.notes.length" @click="DecreaseLimit" href="#" class="show-more">Show less</a><br>
 
   </div>
  </div>
 </div>
 

</template>

<script>
 
 import Personalized from './components/Personalized.vue';
 import UserProfile from './components/UserProfile.vue';
 

export default {
  name: 'App',
  components: {
    Personalized,
    UserProfile,
  
  },

  data() {
    return {
      
        display: "none",
        note: {
      
          title: "",
          description: "",
          date: ""
        },
        user: {
          username: "",
          notes: [

          ]
        },
        
        //This variable will be used for show more feature of our app
        limitNumber: 4
    }
  },

  mounted() {
  
   if (localStorage.getItem('user')) {
      
      this.user = JSON.parse(localStorage.getItem('user'));
    
   } 
  },



  methods: {
    RevealForm: function(){

       this.display = "";
    },

    SumbitForm: function(){
        
        this.display = "none";

        //Get the current date
        var today = new Date();
        var dd = String(today.getDate()).padStart(2, '0');
        var mm = String(today.getMonth() + 1).padStart(2, '0'); //January is 0!
        var yyyy = today.getFullYear();

        //set date format 
        today = dd + '/' + mm + '/' + yyyy;

        this.note.date = today;
        this.user.notes.push(this.note);
       
        localStorage.setItem('user', JSON.stringify(this.user));
        
        //Clean form inputs
        this.note.title = "";
        this.note.description = "";

        this.user = JSON.parse(localStorage.getItem('user'));
    },
    
    //We pass the index of the selected note to be removed here
    RemoveNote: function(note) {
      
      this.user.notes.splice(this.user.notes.indexOf(note),1);

      //Set again the user in local storage since the list of notes has been changed 
      localStorage.setItem('user', JSON.stringify(this.user));
    },

    FetchData($event) {
     
      this.user.username  = $event.username;
      localStorage.setItem('user', JSON.stringify(this.user));
    },

    IncreaseLimit: function() {
        this.limitNumber = this.limitNumber + 2;
    },

    DecreaseLimit: function() {
       this.limitNumber = this.limitNumber - 2;
    },

   

  
  }, 
  computed: {
    notesToShow: function() {
      return this.user.notes.slice(0,this.limitNumber);
    }
  },
   
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.btn-circle {
  width: 30px;
  height: 30px;
  text-align: center;
  padding: 6px 0;
  font-size: 12px;
  line-height: 1.428571429;
  border-radius: 15px;
}
.btn-circle.btn-lg {
  width: 50px;
  height: 50px;
  padding: 10px 16px;
  font-size: 18px;
  line-height: 1.33;
  border-radius: 25px;
}
.btn-circle.btn-xl {
  width: 70px;
  height: 70px;
  padding: 10px 16px;
  font-size: 24px;
  line-height: 1.33;
  border-radius: 35px;
}

#personalize {
  color: #45b6fe;
}
</style>
