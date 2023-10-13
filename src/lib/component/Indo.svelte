<script>
  import { onMount } from 'svelte';
  import {base_api,apikey} from '../../configapi/api.js'
  import {Link} from 'svelte-navigator'
  let videos = []
 let loading = true;
 let totalpages; // Add this line

  let currentpage = 1
  async function getapi(page){
    const response = await fetch(`${base_api}/indo/?key=${apikey}&limit=25&page=${page}`);
    const data = await response.json();
    videos = data.videos;
     totalpages = Math.ceil(data.total / 25); 
     loading = false;
  }

  onMount(async () => {
    await getapi(currentpage)
  });
</script>


{#if loading}
  <!-- Tampilkan spinner atau indikator loading di sini -->
<div style="display:flex;flex-direction:column;justify-content:center;
  margin: 50px;
"
> 
<div class="preloader-wrapper active">
  <div class="spinner-layer spinner-orange-only">
    <div class="circle-clipper left">
      <div class="circle"></div>
    </div><div class="gap-patch">
      <div class="circle"></div>
    </div><div class="circle-clipper right">
      <div class="circle"></div>
    </div>
  </div>
</div>
<br>
<h5 style="color:white">Sedang Mencari data ....</h5>
</div>


{:else}
<div class="row">
  {#each videos as video (video.id)}
    <div class="col m4 xl4 mb-4 s12">
      <div style="margin:10px;padding: 10px;
      background-color: black;border-radius: 30px;
      " class="z-depth-4">
        <Link class="linkto" to={`/player/${video.id}`}>
          <img src={video.image} alt={video.title} 
          style="width:100%;background-size: cover;border-radius: 30px;"
          />
        <div class="card-body">
          <h6 style="font-weight:bold">{video.title}</h6>

          <div style="display:flex;justify-content:space-evenly;">
             <p class="card-text">Durasi : {video.duration}</p>
          <p class="card-text">Diupload : {video.date_formatted}
         </p>
          </div>

          <div style="display:flex;justify-content: end;">
            <!-- ACTION -->
              <Link to={`/player/${video.id}`} class="waves-effect btn waves-light"
              style="background-color: #fabb0f;color: black;
              border-radius: 30px;
              "
              >
              Nonton
            </Link>
          </div>
        </div>
        </Link>

      </div>
    </div>
  {/each}
</div>
<div class="row">
  {#each Array.from({ length: totalpages }, (_, i) => i + 1) as page}
    <li class="pagination-item {page === currentpage ? 'active' : ''}">
      <a on:click={() => gotoPage(page)}>{page}</a>
    </li>
  {/each}
</div>

{/if}

<style>
  
  .spinner-orange-only .circle {
  border-color: #f0e6cc ;
}
</style>
