<script lang="ts">
   import type { RankRequestListing } from '$lib/models/Ranking';
   export let request: RankRequestListing;
   import type SearchView from '$lib/components/common/search.svelte';
   import { searchView } from '$lib/global-store';
   let searchModal: SearchView;

   let songName : string;
   $: songName = `${request.leaderboardInfo.songName}${request.leaderboardInfo.songSubName ? ' ' + request.leaderboardInfo.songSubName : ''}`;

   let truncatedSongName : string;
   $: truncatedSongName = songName.length < 30 ? songName : songName.slice(0, 29).trim() + '…';

   searchView.subscribe((v) => (searchModal = v));

   const openSearch = (val) => {
      searchModal?.setVisibility(true);
      searchModal?.search(val);
   };
</script>

<div class="song-container">
   <div class="song-image-wrapper">
      <img class="song-image" src={request.leaderboardInfo.coverImage} alt="Cover" />
   </div>
   <div class="song-info-container">
      <div class="song-info">
         <a href={`/ranking/request/${request.requestId}`}>
            <span class="song-name" title={truncatedSongName !== songName ? songName : null}>{truncatedSongName}</span>
         </a>
         by
         <a href={'#'}>
            <span>
               {request.leaderboardInfo.songAuthorName.length < 30
                  ? request.leaderboardInfo.songAuthorName
                  : request.leaderboardInfo.songAuthorName.slice(0, 29).trim() + '…'}
            </span>
         </a>
      </div>
      <div class="mapper-info">
         mapped by
         <a href={'#'} on:click={() => openSearch(request.leaderboardInfo.levelAuthorName)}>
            <span class="mapper-name">
               {request.leaderboardInfo.levelAuthorName.length < 30
                  ? request.leaderboardInfo.levelAuthorName
                  : request.leaderboardInfo.levelAuthorName.slice(0, 29).trim() + '…'}
            </span>
         </a>
      </div>
   </div>
</div>

<style>
   .song-name {
      font-weight: 800;
      font-size: larger;
   }
   .song-image {
      min-width: 46px;
      width: 46px;
      height: 46px;
      border-radius: 15%;
      margin-right: 25px;
      display: block;
   }

   .song-info-container {
      display: flex;
      flex-direction: column;
   }
   .song-container {
      display: flex;
   }
   .song-image-wrapper {
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
   }
</style>
