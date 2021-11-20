<template>
    <section class="container recipes">
        <div class="filter">
            <form>
                <input type="text" v-model="search" placeholder="Your ingredient to find recipes..">
            </form>
        </div>

        <div class="list-recipes">
            <div class="content">
                <div class="item" v-for="recipe in filteredRecipes" :key="recipe.title">
                    <div class="photo" style="background-image: url('https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRksltkN9oYX7Z2GDMHtZhcU-FBopa5sSu4AA&usqp=CAU')"></div>
                    <div class="info">
                        <h3>{{recipe.title}}</h3>
                        <ul>
                            <li v-for="(ingredient, index) in recipe.ingredients" :key="index">{{ingredient}}</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import axios from 'axios';

export default {
    name: "content",
    data(){
        return{
            recipes: [],
            search: ''
        }
    },
    async mounted() {
        const response = await axios.get(`http://localhost:3000/recipes`);
        this.recipes = response.data;
    },
    computed:{
        filteredRecipes: function() {
            return this.recipes.filter((recipe) => {
                // return recipe.title.toLowerCase().includes(this.search.toLowerCase());
                // return recipe.title.match(this.search);

                let ingredients = recipe.ingredients.filter((i) => {
                    return i.toLowerCase().indexOf(this.search) > -1
                    // return i.split(',').every(v => this.search.toLowerCase().includes(v.toLowerCase()))
                })
                return ingredients.length > 0
            })
        }
    }
}
</script>

<style scoped>
    /*  */
    section.recipes{
        margin-left: 10px;
    }

    /* filter */
    section.recipes .filter{
        display: flex;
        margin-bottom: 20px;
    }
    section.recipes .filter form{
        display: flex;
        width: 100%;
    }
    section.recipes .filter input{
        width: 100%;
        padding: 15px 20px
    }

    /* list of recipes */
    .list-recipes .content{
        display:flex;
        justify-content: space-between;
        margin-bottom: 30px;
    }
    .list-recipes .content .item{
        width: 32%;
        box-shadow: 0px 0px 3px 0px rgba(0,0,0,0.75);
        border-radius: 10px;
    }
    .list-recipes .content .photo{
        background-size: cover;
        background-position: center center;
        background-repeat: no-repeat;
        aspect-ratio: 210/117;
        border-radius: 10px 10px 0 0;
    }
    .list-recipes .content .info{
        padding: 8px 10px;
    }
    .list-recipes .content .info h3{
        margin: 0;
    }
    .list-recipes .content .info ul{
        padding: 0;
        margin-bottom: 0;
        margin-top: 5px;
        list-style-type: none;
        display: inline-flex;
        flex-wrap: wrap;
    }
    .list-recipes .content .info ul li:after{
        content: ",\00a0";
        display: inline-block;
    }
    .list-recipes .content .info ul li:last-child:after{
        content: "";
        display: inline-block;
    }
</style>