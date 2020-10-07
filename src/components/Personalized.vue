<template>
   <!-- Modal -->
 <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Profile</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
         <div class="form-group">
         <h6 class="profile-label">Username</h6>
         <input type="email" class="form-control"  placeholder="ex John,Obi-wan.." v-model="username">
         </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary" data-dismiss="modal" @click="PassData">Save changes</button>
      </div>
    </div>
    </div>
  </div>
 </div>
</template>
<script>
export default {
    
    data() {
        
        return {
          username: ""
        }
    },

    methods: {
      PassData: function(){
           
        this.$emit('getdata',{'username':this.username});

      }
    }
}

</script>
<style>

  .profile-label {
    text-align: left !important;
  }

</style>