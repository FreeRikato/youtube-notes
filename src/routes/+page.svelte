<script>
    let youtubeUrl = '';
    let thumbnailUrl = '';

    function handleUrlChange(event) {
        youtubeUrl = event.target.value;
    }

    function extractVideoId(url) {
    const regExp = /^.*((youtu.be\/)|(v\/)|(\/u\/\w\/)|(embed\/)|(watch\?))\??v?=?([^#&?]*).*/;
    const match = url.match(regExp);
    return (match && match[7].length === 11) ? match[7] : null;
}


    function fetchThumbnail() {
        const videoId = extractVideoId(youtubeUrl); // You'll need a helper function

        if (videoId) {
            thumbnailUrl = `https://img.youtube.com/vi/${videoId}/0.jpg`; 
        } else {
            thumbnailUrl = ''; // Reset for invalid URLs
        }
    }
</script>

<input type="text" bind:value={youtubeUrl} on:input={handleUrlChange}>
<button on:click={fetchThumbnail}>Fetch Thumbnail</button>

{#if thumbnailUrl}
    <img src={thumbnailUrl} alt="YouTube Thumbnail">
{/if}
