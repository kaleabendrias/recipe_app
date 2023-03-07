<template>

<div id="container">

<heade
:showAddRecipe="showAddRecipe"
@toggle-add-recipe="toggleAddRecipe"
title="Recipe app"/>

<AddRecipe v-show="showAddRecipe" @add-recipe="addRecipe"/>

<Recipes @delete-recipe="deleteRecipe" :recipess="recipiess" />

<foote />

</div>

</template>

<script>
import heade from './components/Header.vue'
import foote from './components/Footer.vue'
import AddRecipe from './components/AddRecipe.vue'
import Recipes from './components/Recipes.vue'
export default{
  name:'app',
  components:{
    heade,
    foote,
    AddRecipe,
    Recipes
  },
  data(){
    return{
    tasks: [],
    showAddRecipe: false,
    recipiess:[]
    }
  },
  methods:{
    toggleAddRecipe(){
      this.showAddRecipe = !this.showAddRecipe
    },
    async deleteRecipe(id){
    if(confirm('Are you sure?')){
      const res = await fetch(`http://localhost:5000/recipies/${id}`, {
        method: 'DELETE'
      })

      res.status === 200 ? 
      this.recipiess = this.recipiess.filter((recipe) => recipe.id != id) : alert("Error deleting recipe")
    }
  },
    async addRecipe(rec){
      console.log(rec)
      const res = await fetch('http://localhost:5000/recipies',{
        method: 'POST',
        headers: {
          'Content-type' : 'application/json',
        },
        body: JSON.stringify(rec)
      })

      const data = await res.json()
      this.recipiess = [...this.recipiess, data]
      console.log('added')
      },
  async fetchrecipies(){
    const res = await fetch('http://localhost:5000/recipies')

    const data = await res.json()
    return data
  }
  },
  async fetchRecipe(id){ 
    const res = await fetch(`http//localhost:5000/recipies/${id}`)

    const data = await res.json()

    return data
  },
  
  async created(){
    this.recipiess = await this.fetchrecipies()
  

  }

}
</script>

<style>
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
#container{
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
  box-shadow: 0 28px 18px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
.btn{
  display: inline-block;
  background: #000;
  color:#fff;
  border:none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;

}
</style>