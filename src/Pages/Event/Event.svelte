<script lang="ts">
  let event = [];

  const getEvent = async () => {
    await fetch("http://103.134.154.200/event")
      .then((res) => res.json())
      .then((data) => {
        console.log(data)
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
            <button class="btn btn-success float-end"   data-bs-toggle="modal"
            data-bs-target="#exampleModal{event._id}">Show More</button>
            <div
            class="modal fade"
            id="exampleModal{event._id}"
            tabindex="-1"
            aria-labelledby="exampleModalLabel"
            aria-hidden="true"
          >
            <div class="modal-dialog">
              <div class="modal-content">
                <div class="modal-body text-center">
                  <p>{event.description}</p>
                  <button class="btn_close btn btn-success" data-bs-dismiss="modal">Close</button>
                </div>
              </div>
            </div>
          </div>
          </div>
        </div>
      </div>
      {/each}
    </div>
  </div>

</div>

<style>
  .btn_close {
    width: 100%!important;
  }
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
