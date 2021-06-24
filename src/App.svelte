<script>
	import Tailwind from "./Tailwind.svelte";
	import MovieInput from "./Components/MovieInput.svelte";
	import MovieList from "./Components/MovieList.svelte";
	import Search from "./Components/Search.svelte";

	//Checks if the object 'movies' exists inside local storage on component load.

	//Ternary conditional statement: parse object to JSON if 'true' to an empty array if 'false'.

	let movies = localStorage.getItem("movies")
		? JSON.parse(localStorage.getItem("movies"))
		: [];

	/* submitMovie function takes a parameter of string 'movie' from input 
	and add it together with the current movie list to local storage. */

	const submitMovie = (movie) => {
		const updatedMovies = [...movies, movie];
		localStorage.setItem("movies", JSON.stringify(updatedMovies));
		movies = updatedMovies;
		alert("Movie successfully added to journal!");
	};

	const clearSearch = () => {
		movies = localStorage.getItem("movies")
			? JSON.parse(localStorage.getItem("movies"))
			: [];
	};

	const search = (searchTerm) => {
		const tempMovies = localStorage.getItem("movies")
			? JSON.parse(localStorage.getItem("movies"))
			: [];
		movies = tempMovies.filter((m) =>
			m.title.toLowerCase().includes(searchTerm.toLowerCase())
		);
	};
</script>

<div class="text-center p-1 w-1/3 max-w-full mx-auto">
	<h1 class="text-5xl mt-5 mb-5 uppercase text-red-400 subpixel-antialiased ">
		Movie Journal
	</h1>

	<Search
		on:search={(event) => search(event.detail.searchTerm)}
		on:clearSearch={clearSearch}
	/>
	<MovieInput on:submitMovie={(event) => submitMovie(event.detail.movie)} />

	<MovieList {movies} />
</div>
