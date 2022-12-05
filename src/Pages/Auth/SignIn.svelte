<script lang="ts">
  let emailHandler: string = "";
  let password: string;
  async function onSubmit(event: Event) {
    event.preventDefault();
    await fetch("http://103.13.207.31:3000/sign-in", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        username: emailHandler,
        password: password,
      }),
    })
      .then((res) => res.json())
      .then(function (data) {
        if (data.status === 200) {
          console.log(data.data);
          localStorage.setItem("id", data.data.id);
          localStorage.setItem("role", data.data.role);

          location.href = "/";
        } else {
          alert(data.message);
        }
      });
  }
</script>

<div class="signup__main">
  <form method="post" on:submit={(e) => onSubmit(e)}>
    <label for="email" class="mb-1">Username</label>
    <input
      class="mb-5"
      type="text"
      name="email"
      id="email"
      bind:value={emailHandler}
      placeholder="Input Your Username..."
    />
    <label class="mb-1" for="password">Password</label>
    <input
      type="password"
      class="mb-5"
      name="password"
      id="password"
      bind:value={password}
      placeholder="Input Your Password..."
    />
    <p>Dont Have account?<a class="link_sign" href="/sign-up">Register</a></p>

    <button class="btn btn-success" type="submit">Sign In</button>
  </form>
</div>

<style module>
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

  .link_sign {
    text-decoration: none;
    color: #ff3e00;
  }
</style>
