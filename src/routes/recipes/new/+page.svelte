<script>
    
    import { createClient } from '@supabase/supabase-js';
import { goto } from '$app/navigation';

const supabase = createClient(
  'https://dgxpzmgpydtsgtodhkgj.supabase.co',
  'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImRneHB6bWdweWR0c2d0b2Roa2dqIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NTk3NTA0NzIsImV4cCI6MjA3NTMyNjQ3Mn0.FMS16SYYiklIwI6knmkxBI1UpnPm6rBBPsiZalSOQsI'
);
    let title = '';
    let description = ''; 
    let ingredients = ''; 
    let instructions = ''; 
    let prep_time = 0; 
    let cook_time = 0; 
    let servings = 4; 
    let loading = false; 

    async function handleSubmit(){
        loading = true; 

        const { data, error } = await supabase
            .from('recipes')
            .insert([
                {
                    title,
                    description,
                    ingredients,
                    instructions,
                    prep_time,
                    cook_time,
                    servings
                }
            ])
            .select(); 
        loading = false;

        if (error)
        {
            alert('Error creating recipe: ' + error.message);
        } 
        else 
        {
            alert('Recipe created!');
            goto('/'); // Naviagates to the homepage after submitting a new recipe 
        }
    }
    
</script>

<div class ="container">
    <h1>Add New Recipe</h1> 

    <form on:submit|preventDefault={handleSubmit}>
        <div>
            <label for="title">Recipe Title</label>
            <input id="title" type="text" bind:value={title} required/>
        </div>

        <div>
            <label for="description">Description</label>
            <textarea id="description" bind:value={description} rows="3" required></textarea>
        </div>

        <div>
            <label for="ingredients">Ingredients</label>
            <textarea id=ingredients bind:value={ingredients} rows="8" required></textarea>
        </div>

        <div>
            <label for="instructions">Instructions</label>
            <textarea id=instructions bind:value={instructions} rows="8" required></textarea>
        </div>

        <div class="row">
            <div>
                <label for="prep_time">Prep Time</label>
                <input id="prep_time" bind:value={prep_time} min="0" />
            </div>

            <div>
                <label for="cook_time">Cook Time</label>
                <input id="cook_time" bind:value={cook_time} min="0" />
            </div>

            <div>
                <label for="servings">Servings</label>
                <input id="servings" bind:value={servings} min="1" />
            </div>
        </div>

        <button type="submit" disabled={loading}>
            {loading ? 'Creating...' : 'Create Recipe'}
        </button> 

        <a href="/">Cancel</a>
    </form>
</div>

<style>
    .container{
        max-width: 800px;
        margin: 0 auto; 
        padding: 2rem;  
    }
    
    form{
        display: flex; 
        flex-direction: column;
        gap: 1.5rem;
    }

    label{
        display: block;
        font-weight: bold; 
        margin-bottom: 1rem; 
    }

    input, textarea{
        width: 100%;
        padding: 0.5rem;
        border: 1px solid #ccc;
        border-radius: 4px; 
        font-family: inherit; 
    }

    .row{
        display: grid; 
        grid-template-columns: repeat(3, 1fr);
        gap: 1rem; 
    }

    button{
        background: #ff3e00; 
        color: white;
        padding: 0.75rem 1.5rem;
        border:none; 
        border-radius: 4px; 
        cursor: pointer; 
        font-size: 1rem
    }

    button:disabled{
        opacity: 0.5;
        cursor: not-allowed;
    }

    a{
        color: #ff3e00;
        text-decoration: none;
        text-align: center; 
    }
</style> 


