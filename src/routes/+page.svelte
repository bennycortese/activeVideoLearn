<script>
    import Youtube from './Youtube.svelte';
    import VideoPlayer from './VideoPlayer.svelte';
  </script>
  
  <style>
    .video-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: (100vh - 40px); /* Full height of the viewport */
      padding: 0px;
    }
  
    .video-player-wrapper {
      width: 80%; /* Adjust this value as needed */
      margin: 0 auto; /* This will center the video player if it has a width less than 100% */
    }
  
    /* Style the input to match your design */
    .input {
      margin-bottom: 0px; /* Spacing between the input and video */
      width: 100%; /* Full width of its container */
      max-width: 400px; /* Maximum width */
    }
  </style>
  
  <div class="video-container">
    <h1>Welcome to SvelteKit</h1>
    <p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the docs</p>
    <div class="video-player-wrapper">
      <VideoPlayer 
        videoSrc="/video5elvaGrc37U.mp4"
      />
      <div class="buttons-container">
        <button class="btn btn-primary">A</button>
        <button class="btn btn-primary">B</button>
        <button class="btn btn-primary">C</button>
        <button class="btn btn-primary">D</button>
      </div>
    </div>
  </div>
  