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
	import MovieCard from '../../../components/MovieCard.svelte';

	let movieDetails = [];

	onMount(async () => {
		try {
			let url = window.location.href;
			// Remove trailing slash if it exists
			if (url.endsWith('/')) {
				url = url.slice(0, -1);
			}
			const idIndex = url.lastIndexOf('/') + 1;
			const id = url.substring(idIndex);

			const res = await fetch(`https://api.themoviedb.org/3/movie/${id}?language=en-US`, options);
			const data = await res.json();
			movieDetails = data;
			console.log(movieDetails);
		} catch (err) {
			console.error('Fetch error: ', err);
		}
	});
</script>

<div class="movie-details">
	<div class="img-container">
		<img
			src={'https://image.tmdb.org/t/p/original/' + movieDetails.backdrop_path}
			alt={movieDetails.title}
		/>
	</div>
	<div class="txt-container">
		<h1>{movieDetails.title}</h1>
		<p class="overview">{movieDetails.overview}</p>
		<p>
			<span>Release date</span>
			{movieDetails.release_date}<br />
			<span>Budget:</span> ${movieDetails.budget}<br />
			<span>Rating:</span>
			{movieDetails.rating}<br />
			<span>Runtime:</span>
			{movieDetails.runtime} mins <br />
		</p>
	</div>
</div>

<style>
	h1 {
		padding: 1rem 0rem 2rem;
	}
	p {
		padding: 1rem 0rem;
	}
	.img-container {
		width: 100%;
	}
	img {
		width: 100%;
		border-radius: 1rem;
	}
	.movie-details {
		margin: 2rem 20%;
	}
	span {
		font-weight: bold;
	}
</style>
