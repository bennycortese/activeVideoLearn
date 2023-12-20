<script>
    export let videoSrc = ''; // URL of the MP4 file
</script>

<style>
    video {
        width: 100%; /* Make video width responsive to the container */
        max-width: 640px; /* Maximum video width */
        height: auto; /* Maintain aspect ratio */
        max-height: 360px; /* Maximum video height */
    }

    .video-container {
        display: flex;
        justify-content: flex-start; /* Aligns content to the top */
        align-items: center;
        padding-top: 20px; /* Adjust this value as needed */
        padding-bottom: 20px; /* Adds some padding at the bottom */
    }
</style>

<div class="video-container">
    <video src={videoSrc} controls>
        Your browser does not support the video tag.
    </video>
</div>
