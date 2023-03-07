<template>
    
  <form class="add-form" @submit="onSubmit">
    <div class="form-control">
      <label>Name</label>
      <input v-model="text" type="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label>Recipe</label>
      <textarea
      v-model="steps"
        type="text"
        name="steps"
        placeholder="Add the recipies"
        rows="9" cols="50"
      />
    </div>

    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>


</template>


<script>
export default{
  name:'AddRecipe',
    data(){
        return{
            text:'',
            steps:'',
        }
    },
    methods:{
        onSubmit(e){
          e.preventDefault()
            if(!this.text){
                alert('Please enter value.')
                return
            }
            const newRecipe = {
              text: this.text,
              steps: this.steps
        }
        this.$emit('add-recipe', newRecipe)

        this.text = ''
        this.steps = ''

        }
        
    }
}
</script>


<style scoped>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>