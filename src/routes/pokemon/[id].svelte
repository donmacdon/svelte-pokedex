<script context="module">
    export async function load({page}){
        const id = page.params.id
        const url = `https://pokeapi.co/api/v2/pokemon/${id}`
        const res = await fetch(url)
        const pokeman = await res.json()
        return {props: {pokeman}}
    }
</script>

<script>
    export let pokeman
    const type = pokeman.types[0].type.name
    const type1 = pokeman.types[1].type.name
</script>

<div class="flex flex-col items-center">
    <h1 class="mt-20">{pokeman.name}</h1>
    <p>Type: <strong class="uppercase">{type}/{type1}</strong> | Height: <strong>{pokeman.height}</strong> | Weight: <strong>{pokeman.weight}</strong></p>
    <img class="card-image" src="{pokeman.sprites['front_default']}" alt="{pokeman.name}">
</div>
