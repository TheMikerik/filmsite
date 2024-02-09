<script>
	export let movie;
</script>

<div class="movie-card">
	<a data-sveltekit-preload-data data-sveltekit-noscroll href={'/movie/' + movie.id}>
		<img src={'https://image.tmdb.org/t/p/w500' + movie.poster_path} alt={movie.title} />
	</a>
	<div class="description">
		<h2>{movie.title}</h2>
		<p>{movie.release_date}</p>
	</div>
</div>

<style>
	img {
		width: 100%;
		object-fit: scale-down;
		border-radius: 1.5rem;
		margin-bottom: 1rem;
	}
	h2 {
		font-size: 1.8rem;
	}
	.description {
		height: 5vh;
	}
	p {
		font-size: 1.4rem;
	}
	.movie-card {
		display: flex;
		flex-direction: column;
		justify-content: space-around;
		padding: 1rem;
	}
</style>
