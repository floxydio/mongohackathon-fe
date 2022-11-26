<script lang="ts">
      import { Link } from "svelte-navigator";

    export let name: string;
    let getId: string = localStorage.getItem("id");
    let getRole: string = localStorage.getItem("role");

    function goToSignIn() {
        alert("Berhasil")
        location.reload()
        localStorage.removeItem("id");
        localStorage.removeItem("role")
    }
</script>

<!-- <nav>
    <h2><Link to="/">{name}</Link></h2>
    <div class="nav-right">
        <Link to="/">Home</Link>
        <Link to="/event">Event</Link>
        {#if getId === null && getRole === null}
        <Link to="/sign-in">Sign In</Link>
        {:else}
        <Link on:click={goToSignIn} to="/">Logout</Link>
        {/if}
    </div>
</nav> -->

<nav class="navbar navbar-expand-lg navbar-light bg-success">
    <div class="container-fluid ">
        <h2 class="navbar-brand"><Link to="/">{name}</Link></h2>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav mx-auto">
          <li class="nav-item">
            <Link class="nav-link text-white" to="/">Home</Link>
          </li>
          <li class="nav-item">
            <Link class="nav-link text-white" to="/event">Event</Link>
          </li>
          <li class="nav-item">
            <Link class="nav-link text-white" to="/about">About</Link>
          </li>
          <li class="nav-item ">
            {#if getId === null && getRole === null}
            <div></div>
            {:else}
              <Link class="nav-link text-white" to="/create-post">Create Post</Link>
            {/if}
          </li>
          <li class="nav-item">
            {#if getId === null && getRole === null}
            <Link class="nav-link text-white" to="/sign-in">Sign In</Link>
            {:else}
            <Link class="nav-link text-white" on:click={goToSignIn} to="/">Logout</Link>
            {/if}
          </li>


        </ul>
      </div>
    </div>
  </nav>


<style>
    nav {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }



    :global(a) {
        color: white;
        margin-left: 10px;
        margin-right: 10px;
        text-decoration: none;
    }
    :global(a):hover {
        transition: 0.3s;
        color: #ff3e00;
    }
</style>
