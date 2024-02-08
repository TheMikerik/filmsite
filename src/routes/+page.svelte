<script context="module">
	const options = {
		method: 'GET',
		headers: {
			accept: 'application/json',
			Authorization:
				'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJhYTA1MDk0ZGRjZDA1ODA2MzVkNmM1YjQ2NDZjODEwMCIsInN1YiI6IjY1YzRiY2JjZmQ2ZmExMDE4Nzc5NjMzMSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.qNpoqAl_bfIGisVodZLJDK_P7_NbB5et_ApnaylGz3I'
		}
	};
	console.log('prefetch');

	async function fetchData() {
		console.log('fetching');
		const options = {
			method: 'GET',
			headers: {
				accept: 'application/json',
				Authorization:
					'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJhYTA1MDk0ZGRjZDA1ODA2MzVkNmM1YjQ2NDZjODEwMCIsInN1YiI6IjY1YzRiY2JjZmQ2ZmExMDE4Nzc5NjMzMSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.qNpoqAl_bfIGisVodZLJDK_P7_NbB5et_ApnaylGz3I'
			}
		};

		try {
			const res = await fetch(
				'https://api.themoviedb.org/3/movie/popular?language=en-US&page=1',
				options
			);
			const data = await res.json();
			console.log(data);
			console.log('fetching done');

			return {
				props: { popular: data.results }
			};
		} catch (err) {
			console.error('Fetch error: ', err);
		}
	}
	export let popular = fetchData();
</script>

<script>
	import PopularMovies from '../components/PopularMovies.svelte';
</script>

<section>
	<PopularMovies {popular} />
</section>
