<script context="module">
	const options = {
		method: 'GET',
		headers: {
			accept: 'application/json',
			Authorization:
				'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJhYTA1MDk0ZGRjZDA1ODA2MzVkNmM1YjQ2NDZjODEwMCIsInN1YiI6IjY1YzRiY2JjZmQ2ZmExMDE4Nzc5NjMzMSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.qNpoqAl_bfIGisVodZLJDK_P7_NbB5et_ApnaylGz3I'
		}
	};
</script>

<script>
	import { onMount } from 'svelte';

	let popular = [];

	onMount(async () => {
		try {
			const res = await fetch(
				'https://api.themoviedb.org/3/movie/popular?language=en-US&page=1',
				options
			);
			const data = await res.json();
			console.log(data);
			popular = data.results;
		} catch (err) {
			console.error('Fetch error: ', err);
		}
	});

	import PopularMovies from '../components/PopularMovies.svelte';
	import SearchMovies from '../components/searchMovies.svelte';
	import global from '../global.css';
	import { fly } from 'svelte/transition';
</script>

{#if popular.length > 0}
	<section in:fly={{ y: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }}>
		<SearchMovies />
		<PopularMovies {popular} />
	</section>
{/if}
