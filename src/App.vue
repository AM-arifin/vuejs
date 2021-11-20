<template>
    <Header />

    <div class="main-content container">
        <Ingredients />
        <Recipes />
    </div>

    <Footer />
</template>

<script>

import Header from "@/components/header.vue"
import Ingredients from "@/components/ingredients.vue"
import Recipes from "@/components/recipes.vue"
import Footer from "@/components/footer.vue"

export default {
    name: 'App',
    components:{
        Header,
        Ingredients,
        Recipes,
        Footer,
    }
}
</script>

<style scoped>
div.main-content{
    display: flex;
}
</style>
