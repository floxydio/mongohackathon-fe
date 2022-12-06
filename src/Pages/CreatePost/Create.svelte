<script>
  import { quill } from "svelte-quill";

  let content;
  let category;
  let title;
  let image;

  function checkLogin() {
    let getId = localStorage.getItem("id");
    let getRole = localStorage.getItem("role");
    if (getId === null && getRole === null) {
      window.location.replace("/");
    }
  }
  checkLogin()

  const onFileSelected = (e) => {
    image = e.target.files[0];
  };

  const options = {
    modules: {
      toolbar: [
        [{ header: [1, 2, 3, false] }],
        ["bold", "italic", "underline", "strike"],
        ["link", "code-block"],
        ["link"],
        [{ list: "ordered" }, { list: "bullet" }],
        [{ align: [] }],
        [{ color: [] }, { background: [] }],
        ["clean"],
      ],
    },
    placeholder: "Type something...",
    theme: "snow",
  };

  async function callContent() {
    const formData = new FormData();

    formData.append("title", title);
    formData.append("category", category);
    formData.append("content", content.html);
    formData.append("image", image);

    await fetch("http://103.134.154.200/create", {
      method: "POST",

      body: formData,
    })
      .then((res) => res.json())
      .then((data) => window.location.replace("/"))
      .catch((err) => alert(err));
  }
</script>

<div class="create_post">
  <input
    class="input_category"
    type="text"
    placeholder="Title?"
    bind:value={category}
  />
  <label for="file">Image for Thumbnail</label>
  <input
    class="input__file"
    type="file"
    accept=".jpg, .jpeg, .png"
    alt="Submit"
    width="48"
    height="48"
    on:change={(e) => onFileSelected(e)}
  />
  <label for="select">Select Category</label>
  <select class="category__input" bind:value={title}>
    <option value="Tech">Tech</option>
    <option value="Lifestyle">Lifestyle</option>
    <option value="Cooking">Cooking</option>
  </select>
  <div
    class="editor"
    on:text-change={(e) => (content = e.detail)}
    use:quill={options}
  />
  <button class="btn_post" on:click={callContent}>Post Content</button>
</div>

<style>
  .create_post {
    margin-top: 60px;
    margin-bottom: 20px;
  }
  .category__input {
    margin-top: 10px;
    margin-bottom: 20px;
    display: block;
    width: 300px;
  }
  .input__file {
    width: 100%;
    margin-top: 10px;
    margin-bottom: 30px;
  }
  .input_category {
    width: 100%;
    height: 50px;
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 0 10px;
    margin-bottom: 10px;
  }
  .btn_post {
    margin-top: 20px;
    width: 200px;
    height: 40px;
  }
  .create_post {
    margin-left: 20px;
    margin-right: 20px;
  }
  .editor {
    height: 250px;
  }
</style>
