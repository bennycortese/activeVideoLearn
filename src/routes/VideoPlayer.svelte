<script lang="ts">
    import { onDestroy } from 'svelte';
    export let videoSrc = ''; // URL of the MP4 file
    let video : HTMLVideoElement;
    let targetTime = 10; // The timestamp in seconds when you want to trigger the event

    // A reactive statement that sets up the event listener
    // when the video element is mounted to the DOM
    $: {
      if (video) {
        video.addEventListener('timeupdate', handleTimeUpdate);
      }
    }

    function handleTimeUpdate(event: Event): void {
      if (video.currentTime >= targetTime) {
        console.log(`Reached ${targetTime} seconds!`);
        video.removeEventListener('timeupdate', handleTimeUpdate); // Optional: remove if you want it to trigger every time
        // Add your logic for what should happen at this time
      }
    }

    // Cleanup when the component is destroyed
    onDestroy(() => {
      if (video) {
        video.removeEventListener('timeupdate', handleTimeUpdate);
      }
    });
</script>

<svelte:head>
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
</svelte:head>

<div class="video-container">
    <video bind:this={video} src={videoSrc} controls>
        Your browser does not support the video tag.
    </video>
</div>
