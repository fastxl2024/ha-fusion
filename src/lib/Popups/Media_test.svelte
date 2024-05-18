<script>
    let mediaItems = [];

    // Fetch media data from Home Assistant
    async function fetchMedia() {
        try {
            let response = await fetch('http://10.73.27.2/api/media');
            if (response.ok) {
                mediaItems = await response.json();
            } else {
                console.error('Failed to fetch media:', response.statusText);
            }
        } catch (error) {
            console.error('Error fetching media:', error);
        }
    }

    fetchMedia();
</script>

<style>
    /* Your CSS styles here */
</style>

<div>
    <h1>Media Browser</h1>

    <ul>
        {#each mediaItems as mediaItem}
            <li>{mediaItem.name}</li>
        {/each}
    </ul>
</div>