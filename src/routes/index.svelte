<script context="module">
    export async function load({page}){
        const url = 'https://pokeapi.co/api/v2/pokemon?limit=151'
        const res = await fetch(url)
        const data = await res.json()
        const loadedPokemon = data.results.map((data,index)=>{
            return{
                name: data.name,
                id: index + 1,
                image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index+1}.png`
            }
        })
        return {props: {pokemon:loadedPokemon}}
    }
</script>

<script>
    export let pokemon
    import PokemanCard from "../components/pokemanCard.svelte";

    let searchTerm = ""
    let filterdPokemon = []

    // reactive f(x) of the searchbar when searchterm inputbox is changed
    $: {
        if(searchTerm){
            //search pokemn
            filterdPokemon = pokemon.filter(pokeman => pokeman.name.toLowerCase().includes(searchTerm.toLowerCase()))
        
        }else{
            filterdPokemon = [... pokemon]
        }
    }
</script>

<svelte:head>
    <title>Sveltekit Pokedex</title>
</svelte:head>

<h1 class="text-4xl text-center my-8 uppercase">SvelteKit Pokedex</h1>

<input class="w-full rounded-md text-lg p-4 border-2 border-gray-200" type="text" placeholder="Search Pokemon" bind:value="{searchTerm}">

<div class="py-4 grid gap-4 md:grid-cols-2 grid-cols-1">
    {#each filterdPokemon as pokeman}
    <PokemanCard pokeman={pokeman}/>
    {/each}
</div>