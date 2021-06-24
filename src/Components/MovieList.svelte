<script>
    export let movies;
</script>

{#each movies as movie}
    <div
        class="flex flex-col lg:flex-row border mb-2 shadow-lg border-gray-100"
    >
        {#if movie.imageUrl == ""}
            <img
                class="block h-auto w-full lg:w-48 flex-none bg-cover h-24 border"
                alt="No Pic"
                src="https://www.pieceofart.ca/wp-content/uploads/woocommerce-placeholder-600x600.png"
            />
        {:else}
            <img
                class="block h-auto w-full lg:w-48 flex-none bg-cover h-24"
                alt="Movie Cover"
                src={movie.imageUrl}
            />
        {/if}

        <div
            class="bg-white rounded-b lg:rounded-b-none lg:rounded-r p-4 lg:text-left flex flex-col justify-between leading-normal"
        >
            <div class="text-black font-bold text-xl mb-2 mt-5">
                {movie.title}
            </div>

            <span>
                You Rated it:
                {#each { length: movie.rating } as _, i}
                    <span class="inline">⭐</span>
                {/each}
            </span>
        </div>
    </div>
{/each}
