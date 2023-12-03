<script >
	import {Link,navigate} from 'svelte-navigator'
</script>
<div style="background-color: black;color: white;">
	<div style="display: flex;justify-content: space-evenly;"
	class="p-1 shadow" 
	>
		<h5 style="font-weight: bold;" on:click={()=>navigate("/")}>Bang MEKI</h5>
		<Link to="/" class="waves-effect btn"
		style="background-color: red;color: white;"
		>
		Beranda
	</Link>

		<Link to="/request" class="waves-effect btn"
		style="background-color: #ffa805;color: black;"
		>
		Request Bokep
	</Link>
	</div>
</div>


