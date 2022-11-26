<script lang="ts">
  let homeContent = [];

  async function getContent() {
    await fetch("http://192.168.43.110:3000/content")
      .then((res) => res.json())
      .then((data) => (homeContent = data.data));
  }
  getContent();
</script>

<div>
  <div class="container mg-5">
    <div class="row">
      {#each homeContent as event}
        <div class="col-md-4 mb-3">
          <div class="card">
            <img
              src="http://192.168.43.110:3000/static/{event.filename}"
              class="card-img-top img"
              alt="..."
              height="200"
            />
            <div class="card-body">
              <h5 class="event__title">{event.category}</h5>
              <p class="btn_title btn btn-danger">{event.title}</p>
              <div class="content_style">{@html event.content}</div>
              <button
                class="btn btn-success float-end"
                data-bs-toggle="modal"
                data-bs-target="#exampleModal{event._id}">Show More</button
              >
            </div>
            <div
              class="modal fade"
              id="exampleModal{event._id}"
              tabindex="-1"
              aria-labelledby="exampleModalLabel"
              aria-hidden="true"
            >
              <div class="modal-dialog">
                <div class="modal-content">
                  <div class="modal-body">
                    {@html event.content}
                    <button class="btn_close btn btn-success" data-bs-dismiss="modal">Close</button>
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
  .btn_title {
    font-size: 11px;
    width: 80px!important;
    height: 25px;
    border-radius: 20px;
  }
    .btn_close {
    width: 100%!important;
  }
  .content_style {
    overflow: hidden !important;
    text-overflow: ellipsis;
    height: 100px;
    margin-bottom: 20px;
  }
  .mg-5 {
    margin-top: 100px;
  }
  .event__title {
    font-weight: bold  ;
    white-space: nowrap;
    overflow: hidden !important;
    text-overflow: ellipsis;
    font-size: 18px;
    margin-bottom: 10px;
  }
</style>
