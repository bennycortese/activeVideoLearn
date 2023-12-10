<script context="module" lang="ts">
    // Extend the Window interface for TypeScript
    declare global {
      interface Window {
        onYouTubeIframeAPIReady: () => void;
      }
    }
  </script>
  

  <script lang="ts">
    import { onMount, createEventDispatcher } from 'svelte';
    export let videoId: string;
    let player: YT.Player;
    let divId: string = 'player_' + (Math.random() * 109999).toString();
  
    const dispatch = createEventDispatcher();
    let apiReady: boolean = false;
  
    onMount(() => {
      let tag: HTMLScriptElement = document.createElement('script');
      tag.src = "https://www.youtube.com/iframe_api";
      let firstScriptTag: HTMLScriptElement | null = document.getElementsByTagName('script')[0];
      firstScriptTag.parentNode?.insertBefore(tag, firstScriptTag);
  
      window.onYouTubeIframeAPIReady = () => {
        window.dispatchEvent(new Event('youtubeIframeAPIReady'));
      };
  
      window.addEventListener('youtubeIframeAPIReady', () => {
        apiReady = true;
        initializePlayer();
      });
    });
  
    function initializePlayer() {
      if (apiReady) {
        console.log('Initializing YouTube Player for div:', divId);
        player = new YT.Player(divId, {
          height: '390',
          width: '640',
          videoId: videoId,
          events: {
            onReady: playerIsReady,
            onStateChange: playerStateChange
          }
        });
      }
    }
  
    function playerStateChange(event: YT.OnStateChangeEvent): void {
      const data: number = event.data;
      dispatch("PlayerStateChange", data)
      console.log(data)
      let strReturn: string = "";
      if(data === YT.PlayerState.UNSTARTED) { strReturn = "(unstarted)" }
      if(data === YT.PlayerState.ENDED) { strReturn = "(ended)" }
      if(data === YT.PlayerState.PLAYING) { strReturn = "(playing)" }
      if(data === YT.PlayerState.PAUSED) { strReturn = "(paused)" }
      if(data === YT.PlayerState.BUFFERING) { strReturn = "(buffering)" }
      if(data === YT.PlayerState.CUED) { strReturn = "(video cued)." }
      dispatch("PlayerStateChangeString", strReturn)
    }
  
    function playerIsReady(): void {
      dispatch("Ready");
      setInterval(() => {
        dispatch("currentPlayTime", player.getCurrentTime());
        //console.log(player.getCurrentTime())
      }, 1000);
    }
  </script>
  
  <div id={divId} />
  