<script>
    import {quill} from "svelte-quill";

    const options = {
        modules: {
            toolbar: [
                [{header: [1, 2, 3, false]}],
                ["bold", "italic", "underline", "strike"],
                ["link", "code-block"],
                [ 'link', 'image'],
                [{list: "ordered"}, {list: "bullet"}],
                [{align: []}],
                [{color: []}, {background: []}],
                ["clean"],
            ]
        },
        placeholder: "Type something...",
        theme: "snow"
    }
    let content;
    let category;
    let title;
    async function callContent() {
        await fetch("http://192.168.43.110:3000/create", {
            method: "POST",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify({
                title: title,
                category: category,
                content: content.html
            })
        }).then(res => res.json())
            .then(data => console.log(data))
            .catch(err => alert(err))

    }
</script>

<div class="create_post">
    <input class="input_category" type="text" placeholder="Title?" bind:value={category} />
    <select bind:value={title}>
        <option value="Tech">Tech</option>
        <option value="Lifestyle">Lifestyle</option>
        <option value="Cooking">Cooking</option>
    </select>
    <div class="editor" on:text-change={e => content =
    e.detail} use:quill={options}></div>
    <button class="btn_post" on:click={callContent}>Post Content</button>
</div>

<style>
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
        height: 300px;

    }
</style>