<template>
    <div class="recipe">
        <h3>
            {{  recipe.text }}
            <i  @click="onDelete(recipe.id)" class="fas fa-times"></i>
        </h3>
        <p>{{ recipe.steps }}</p>
    </div>
</template>

<script>
export default{
    name:'Recipe',
    props: {
        recipe:Object
    },
    methods:{
        onDelete(id){
            this.$emit('delete-recipe', id)
        }
    }
}
</script>

<style scoped >

.fas{
    color:red;
}
.recipe{
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
}

.recipe h3{
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>
