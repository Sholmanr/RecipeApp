<script>
let recipes = []
</script> 

<div class = "container">
    <h1>Recipes</h1>
    <a href="/recipes/new">Add New Recipe</a>

    <div class = "recipes">
        {#if recipes.length === 0}
            <p>No recipes yet</p>
        {/if}
    </div>
</div>

<style>
        .container{
            max-width: 1200px; 
            margin: 0 auto; 
            padding: 2rem;
        }

    h1{
        color: #333; 
    }

    a{
        display: inline-block;
        background: #ff3e00;
        color: white;
        padding: 0.5rem 1rem; 
        text-decoration: none; 
        border-radius: 4px; 
        margin: 0.5rem 0; 
    }
</style>