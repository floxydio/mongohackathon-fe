<script lang="ts">
  let event = [];

  const getEvent = async () => {
    await fetch("http://192.168.43.110:3000/event")
      .then((res) => res.json())
      .then((data) => {
        event = data.data;
      });
  };

  getEvent();
</script>

<div>
  <!-- <div class="event__div">
    {#each event as event}
    <div class="event__main">
      <img src={event.image_url} alt="" />
      <h2 class="event__title">
        {event.name}
      </h2>
      <span class="event__desc">{event.description}</span>
    </div>
  {/each} -->
  <!-- </div> -->
  <div class="container mt-5">
    <div class="row">
      {#each event as event}
      <div class="col-md-4 mb-3">
        <div class="card">
          <img src={event.image_url} class="card-img-top img" alt="..." height="200" />
          <div class="card-body">
            <h5 class="event__title">{event.name}</h5>
            <p class="event__desc">{event.description}</p>
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
  .event__desc {
    color: gray;
    overflow: hidden !important;
    text-overflow: ellipsis;
    height: 100px;
  }
  .img {
    border-radius: 10px;

  }
</style>
