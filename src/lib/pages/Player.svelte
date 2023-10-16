<script>
  export let id;
  import { onMount } from 'svelte';
  import { Link } from 'svelte-navigator';
  import {base_api,apikey} from '../../configapi/api.js'
  let loading = true;
  let relatedVideos = [];

  let max_page = 46
  
  async function related() {
  const jepang_url = "https://corsany-1-g0403094.deta.app/https://poophd.com/api/list?key=raQu2lrd&folder=9DVR9eBBSMH";
  const indo_url = "https://corsany-1-g0403094.deta.app/https://poophd.com/api/list?key=raQu2lrd&folder=ropbn60oORX";
  const page_select = Math.floor(Math.random() * max_page) + 1; // Menghasilkan angka acak antara 1 hingga 46

  loading = true; // Menampilkan indikator loading

  try {
    const selected_url = Math.random() < 0.5 ? indo_url : jepang_url; // Memilih URL secara acak
    const response = await fetch(`${selected_url}&page=${page_select}` ); // Mengambil data dengan URL terpilih dan nomor halaman terpilih
    const data = await response.json();
    relatedVideos = data.videos;
  } catch (error) {
    console.error("Gagal mengambil video terkait:", error);
  } finally {
    loading = false; // Sembunyikan indikator loading setelah data diambil
  }
}


  onMount(() => {
    related();
  });

  function gotopage(myid) {
    id = myid;
    related();
  }
</script>

<div>
	<div class="container" style="margin-top: 10px;">
	<Link to="/" class="waves-effect btn "
	style="background-color: #e68c07;font-weight: bold;"
	>
	Kembali
</Link>
</div>
	<div style="margin-top:10px">
		<iframe src={`https://poop.mom/e/${id}`}
		allowfullscreen width="100%" height="280px"
		allowscrolling="no" 
		></iframe>
	</div>

	<!-- TOMBOL DOWNLOAD -->
	<div style="margin:10px">
		<button 
		disabled 
		class="waves-effect btn"
		style="width: 100%;
		background-color: #e68c07;color:black;font-weight: bold;
		"> Download Video belum Tersedia </button>
	</div>

	<!-- RELATED -->
	<div style="margin:10px">
		<h5 style="font-weight:bold;color: white;">Video Lainnya</h5>
	</div>

		<div id="related" class="row">
	{#if loading}
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
		<br>
		<p>Jika Terlalu lama bisa refresh kembali atau close buka lagi</p>
		</div>
	{:else}
	  {#each relatedVideos as video (video.id)}
	    <div class="col m4 xl4 s12" >
	      <div class="card" on:click={()=>gotopage(video.id)}>
	        <div class="card-image">
	          <img src={video.image} alt={video.title} style="width:100%;background-size:cover;">
	        </div>
	        <div class="card-content" style="color:white;background-color:black">
	          <span style="font-size: 15px;font-weight: bold">{video.title}</span>
	          <p>Durasi: {video.duration}</p>
	          
	          <div style="display:flex;justify-content:space-evenly;">
	          	<p>Views: {video.views}</p>
	          <p>Tanggal: {video.date_formatted}</p>
	          </div>
	        </div>
	        <div  style="background-color:#ff9903;padding:10px">
	          <button 
	          style="color: black;font-weight: bold;
	          text-align: center;font-size: 18px;
	          background-color:#ff9903;border:0px;
	          "
	          on:click={()=>gotopage(video.id)}>Nonton Sekarang</button>
	        </div>
	      </div>
	    </div>
	  {/each}
	 {/if}
	</div>
</div>

<style>
  
  .spinner-orange-only .circle {
  border-color: #f0e6cc ;
}
</style>
