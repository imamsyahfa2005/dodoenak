<script >
import Indo from '../component/Indo.svelte' 
import Jepang from '../component/Jepang.svelte' 
import Barat from '../component/Barat.svelte'	
 

 let activeTab = 1; // Menentukan tab aktif secara default

  function setActiveTab(tabNumber) {
    activeTab = tabNumber;
  }

</script>


<div>

<div class="tab-container" style="margin:10px">
  <div class="tab " on:click={() => setActiveTab(1)}>INDO</div>
  <div class="tab" on:click={() => setActiveTab(2)}>Jepang</div>
<div class="tab" on:click={() => setActiveTab(3)}>Barat</div>

  <!-- Tambahkan tab lain sesuai kebutuhan -->
</div>

	<div class="content">
  {#if activeTab === 1}
  <div style="margin:10px">
  	<h5 style="color:#f5b505;font-weight: bold;">Bokep Indo</h5>
  </div>
    <Indo />
  {:else if activeTab === 2}
     <div style="margin:10px">
    <h5 style="color:#f5b505;font-weight: bold;">Bokep Jepang</h5>
  </div>
    <Jepang />
  {:else if activeTab === 3}
    <div style="margin:10px">
    <h5 style="color:#f5b505;font-weight: bold;">Bokep Barat</h5>
  </div>
    <Barat />
    
  <!-- Tambahkan blok lain untuk komponen tambahan -->
  {/if}
</div>
</div>

<style>
  .tab-container {
    display: flex;
    overflow-x: auto; /* Aktifkan scroll horizontal */
    white-space: nowrap; /* Hindari wrapping ke baris berikutnya */
  }

  .tab {
    padding: 10px 20px;
    cursor: pointer;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin-right: 10px;
    font-weight: bold;
  }

  

  .content {
    width: 100%; /* Pastikan konten memenuhi lebar */
    overflow-x: hidden; /* Sembunyikan scrollbar horizontal di dalam konten */
  }
</style>