<script context="module" lang="ts">
	export async function load() {
		const url = `https://pokeapi.co/api/v2/pokemon?limit=150`;
		const res = await fetch(url);
		const data = await res.json();
		const loadedPokemon = data.results.map((data, index) => {
			return {
				name: data.name,
				id: index + 1,
				image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index + 1}.png`,
			}
		})
		return {props:{pokemon:loadedPokemon}};
	}
</script>
<script lang="ts">
	export let pokemon;
	import PokemanCard from '../components/pokemanCard.svelte';

	let searchTerm = '';
	let filteredPokemon = [];
	$: {
		if (searchTerm) {
			filteredPokemon = pokemon.filter(pokemon => pokemon.name.toLowerCase().includes(searchTerm.toLowerCase()));
		} else {
			filteredPokemon = [...pokemon]
		}
	}

</script>
<svelte:head>
	<title>Svelte kit PokeDex</title>
</svelte:head>
<h1 class='text-4xl text-center my-8 uppercase'>Svelte kit Pokedex</h1>

<input class='w-full rounded-md text-lg p-4 border-2 border-gray-200'
			 bind:value={searchTerm}
			 placeholder='Search Pokemon'
>

<div class='py-4 grid gap-4 md:grid-cols-2 grid-cols-1'>
{#each filteredPokemon as pokeman}
	<PokemanCard {pokeman}/>
{/each}
</div>