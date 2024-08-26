<script>
    import { onMount } from "svelte";

  let song_list = [];

  async function api_call(){
    let res = await fetch("api/getSongs")

    return await res.json()
  }
  onMount(()=>{
    song_list = api_call()
  })
</script>

<main class="flex flex-col gap-5 p-5">
{#await song_list}
    <p>loading...</p>
{:then songs}
  {#each songs as song}
        <a href="{song.direct_download_link}" class="block card card-hover p-4">{song.name + " - " + song.size}</a>
  {/each}
{/await}
</main>
