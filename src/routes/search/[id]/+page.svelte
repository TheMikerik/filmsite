<script context="module">
	const options = {
		method: 'GET',
		headers: {
			accept: 'application/json',
			Authorization: import.meta.env.VITE_API
		}
	};
</script>

<script>
	import { onMount } from 'svelte';

	export let searchedMovie = [];

	onMount(async () => {
		try {
			let url = window.location.href;
			if (url.endsWith('/')) {
				url = url.slice(0, -1);
			}
			const idIndex = url.lastIndexOf('/') + 1;
			const id = url.substring(idIndex);

			const res = await fetch(`https://api.themoviedb.org/3/search/movie?query=${id}`, options);
			const data = await res.json();
			searchedMovie = data.results;
			console.log(searchedMovie);
		} catch (err) {
			console.error('Fetch error: ', err);
		}
	});

	import MovieCard from '../../../components/MovieCard.svelte';
	import.meta.env.VITE_API;
</script>

<div class="searched-movies">
	{#each searchedMovie as movie}
		<MovieCard {movie} />
	{/each}
</div>

<style>
	.searched-movies {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		column-gap: 1rem;
		row-gap: 2rem;
		height: 20vh;
	}
</style>
