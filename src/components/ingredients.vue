<template>
    <section class="container ingredients">
        <div class="filter">
            <form>
                <input type="text" v-model="search" placeholder="Search ingredients..">
            </form>
        </div>
        <div class="table">
            <table>
                <thead>
                    <tr>
                        <th>Title</th>
                        <th>Use by</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="ingredient in filterIngredients" :key="ingredient.title">
                        <td>{{ingredient.title}}</td>
                        <td>{{ingredient.useby}}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </section>
</template>

<script>
import axios from 'axios';

export default {
    name: "content",
    data(){
        return{
            ingredients: [],
            search: ''
        }
    },
    async mounted() {
        const response = await axios.get(`http://localhost:3000/ingredients`);
        this.ingredients = response.data;
    },
    computed:{
        filterIngredients: function() {
            return this.ingredients.filter((ingredient) => {
                return ingredient.title.match(this.search);
            })
        }
    }
}
</script>

<style scoped>
    /*  */
    section.ingredients {
        margin-right: 10px;
    }

    /* filter */
    section.ingredients .filter{
        display: flex;
        margin-bottom: 20px;
    }
    section.ingredients .filter form{
        display: flex;
        width: 100%;
    }
    section.ingredients .filter input{
        width: 100%;
        padding: 15px 20px
    }

    /* list of data on table */
    section.ingredients table{
        width: 100%;
        border: 1px solid gray;
        border-collapse: collapse;
        text-align: left;
    }
    section.ingredients table thead tr th,
    section.ingredients table tbody tr td{
        padding: 13px 20px;
    }
    section.ingredients table thead tr th{
        border-bottom: 1px solid gray;
    }
    section.ingredients table tbody tr:nth-child(even) {
        background-color: #f2f2f2;
    }
</style>