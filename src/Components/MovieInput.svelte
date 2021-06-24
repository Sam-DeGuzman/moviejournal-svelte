<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    let title = "";
    let titleStr = "";
    let imageUrl = "";
    let rating = 1;

    const onTitleChange = (e) => {
        titleStr = e.target.value;
        title = capitalizeFirstLetter(titleStr);
    };

    const onImgUrlChange = (e) => {
        imageUrl = e.target.value;
    };

    const onRatingSelect = (e) => {
        rating = e.target.value;
    };

    const submitMovie = () => {
        if (title) {
            dispatch("submitMovie", {
                movie: {
                    title,
                    imageUrl,
                    rating,
                },
            });

            title = "";
            imageUrl = "";
            rating = 1;
        }
    };

    function capitalizeFirstLetter(string) {
        return string.charAt(0).toUpperCase() + string.slice(1);
    }
</script>

<h3>Add a New Movie to Journal</h3>
<input
    placeholder="Cover Image URL (Optional)"
    type="text"
    value={imageUrl}
    on:keyup={onImgUrlChange}
    class="p-2 w-full mb-3"
/>
<div class="main mb-5">
    <input
        placeholder="Movie Title"
        type="text"
        value={title}
        on:keyup={onTitleChange}
        class="p-2"
    />

    <span class="pt-2 ml-2 -mr-2">⭐</span>
    <!-- svelte-ignore a11y-no-onchange -->
    <select on:change={onRatingSelect}>
        <option value={1}>1</option>
        <option value={2}>2</option>
        <option value={3}>3</option>
        <option value={4}>4</option>
        <option value={5}>5</option>
    </select>

    <button
        on:click={submitMovie}
        disabled={!title}
        class=" text-blue-500 rounded-sm "
        >Submit
    </button>
</div>

<style>
    .main {
        width: 100%;
        display: flex;
    }

    .main input {
        flex: 1;
    }

    .main select {
        width: 75px;
        margin-right: 10px;
        margin-left: 10px;
    }

    .main button {
        width: 75px;
    }
</style>
