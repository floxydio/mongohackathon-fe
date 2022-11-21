<script lang="ts">
  let homeContent = [];

  async function getContent() {
    await fetch('http://192.168.43.110:3000/content').then((res) => res.json()).then((data) => homeContent = data.data);

  }
  getContent();


</script>

<div>
  <div class="container mt-5">
    <div class="row">
      {#each homeContent as event}
        <div class="col-md-4 mb-3">
          <div class="card">
            <img src={event.image_url} class="card-img-top img" alt="..." height="200" />
            <div class="card-body">
              <h5 class="event__title">{event.category}</h5>
              <div>{@html event.content}</div>
              <a href="/" class="btn btn-primary float-end">Show More</a>
            </div>
          </div>
        </div>
      {/each}
    </div>
  </div>
</div>

<style>
  .event__title {
    white-space: nowrap;
    overflow: hidden !important;
    text-overflow: ellipsis;
    font-size: 18px;
    margin-bottom: 10px;
  }
</style>
