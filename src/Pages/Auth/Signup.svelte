<script lang="ts">
    let name: string
    let emailHandler: string = "";
    let password: string;
    async function onSubmit(event: Event) {
        event.preventDefault();
        await fetch("http://103.13.207.31:3000/sign-up ", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({
                name: name,
                username: emailHandler,
                password: password,
                role: 1
            }),
        }).then((res) => res.json()).then(function(data) {
            if(data.status === 201) {
                alert(data.message)
                location.href = "/sign-in";

            }
        });
    }
</script>

<div class="signup__main">
    <form method="post" on:submit={(e) => onSubmit(e)}>
        <label for="name" class="mb-1">Name</label>
        <input class="mb-5" type="text" name="name" id="name" bind:value={name} placeholder="Input Your Name..." />
        <label for="email" class="mb-1">Username</label>
        <input class="mb-5" type="text" name="email" id="email" bind:value={emailHandler} placeholder="Input Your Username..." />
        <label class="mb-1" for="password">Password</label>
        <input type="password" class="mb-5" name="password" id="password" bind:value={password} placeholder="Input Your Password..." />
        <button class="btn btn-success" type="submit">Create Account</button>
    </form>
</div>

<style>
    .mb-5 {
        margin-bottom: 30px;
    }
    .mb-1 {
        margin-bottom: 10px;
    }
    .signup__main {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 80vh;
    }

    .signup__main label {
        font-size: 20px;
    }

    .signup__main form {
        width: 400px;
        text-align: center;
        display: flex;
        flex-direction: column;
    }

    .signup__main input {
        width: 100%;
        padding: 10px;
        border: 1px solid #ccc;
        border-radius: 5px;
    }

    .signup__main input:focus {
        outline: none;
        transition: 0.3s;
        border: 2px solid #ff3e00;
    }

    .signup__main button {
        width: 106%;
        padding: 10px;
        border: none;
        /* background-color: #ff3e00; */
        color: white;
        font-weight: bold;
        cursor: pointer;
    }

    .signup__main button:hover {
        transition: 0.3s;
        background-color: #ff5e00;
    }
</style>
