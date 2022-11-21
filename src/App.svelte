<script lang="ts">
  import Navbar from "./Components/Navbar.svelte";
  import { Router, Route, Link } from "svelte-navigator";
  import Home from "./Pages/Content/Home.svelte";
  import About from "./Pages/About/About.svelte";
  import Event from "./Pages/Event/Event.svelte";
  import SignIn from "./Pages/Auth/SignIn.svelte";
  import Signup from "./Pages/Auth/Signup.svelte";
  import Create from "./Pages/CreatePost/Create.svelte"

</script>
  <Router>
    <Navbar name="FLOXBLOG" />
    <Route path="/" component={Home} />
    <Route path="/about" component={About} />
    <Route path="/event" component={Event} />
    <Route path="/sign-in" component={SignIn} />
    <Route path="/sign-up" component={Signup} />
    <Route path="/create-post" component={Create} />
  </Router>
<style>
</style>