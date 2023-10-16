<script>
  import { Router, Link, Route } from "svelte-navigator";
  import Home from './lib/pages/Home.svelte'
  import Player from './lib/pages/Player.svelte'
  import Request from './lib/pages/Request.svelte'
  import Permintaan from './lib/pages/Permintaan.svelte'

  import Navbarmenu from './lib/utils/Navbarmenu.svelte'
</script>


<Router>
    <div style="background-color:#42424a;">
    <Navbarmenu/>
  <div>
    <Route path="/">
      <Home />
    </Route>
    <Route path="/permintaan">
      <Permintaan />
    </Route>
     <Route path="/request">
      <Request />
    </Route>
    <Route path="/player/:id" let:params>
      <Player id={params.id} />
    </Route>
    </div>
  </div>
</Router>