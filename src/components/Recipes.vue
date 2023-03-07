<template>
    <div>
        <div :key="recipe.id" v-for="recipe in recipess" >
            <Recipe 
            @delete-recipe="$emit('delete-recipe', recipe.id)" 
            :recipe="recipe"/>
        </div>
    </div>
</template>

<script>
import Recipe from './Recipe.vue'
export default{
components:{
    Recipe
},
props:{
    recipess: Array
},
emits:['delete-recipe']
}
</script>
