<template>
  <form>  
    <div class="form-group">
      <label for="workInput">Add Work Name</label>
      <input
        type="text"
        class="form-control"
        id="exampleInputEmail1" 
        v-model="work.workName"      
      />
    </div>
    <button class="btn btn-primary" @click="clickSave()">Save</button>
  </form>
</template>

<script>
export default {
    name:'EditToDo',
    props:{
        work:Object
    },
    methods: {
        clickSave(){
            this.$emit('save', this.work)
        }
    }
}
</script>

<style>

</style>