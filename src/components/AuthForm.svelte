<script>
  export let auth;
  let mode = "signIn";
  let email = "";
  let password = "";

  async function handleSubmit() {
    try {
      if (mode === "signIn") {
        await auth.signInWithEmailAndPassword(email, password);
      } else {
        await auth.createUserWithEmailAndPassword(email, password);
      }
      email = "";
      password = "";
    } catch {
      prompt("Error While trying to validate login, try again later");
    }
  }
</script>

<h1 class="title has-text-info has-text-centered">Mental Chat</h1>
{#if mode === "signIn"}
  <h2 class="title">Sign In</h2>
{:else}
  <h2 class="title">Sign Up</h2>
{/if}

<form on:submit|preventDefault={handleSubmit}>
  <div class="field">
    <div class="field">
      <label class="label">Email</label>
      <div class="control has-icons-left has-icons-right">
        <input
          class={email.includes("@gmail.com")
            ? "input is-success"
            : "input is-danger"}
          type="email"
          placeholder="Email input"
          bind:value={email}
        />
        <span class="icon is-small is-left">
          <i class="fas fa-envelope" />
        </span>
        {#if !email.includes("@gmail.com")}
          <span class="icon has-text-danger is-right">
            <i class="fas fa-exclamation-triangle" />
          </span>
        {:else}
          <span class="icon has-text-success is-right">
            <i class="fas fa-check-square" />
          </span>
        {/if}
      </div>
      {#if email.includes("@gmail.com")}
        <p class={"help is-success"}>This Email is Available</p>
      {:else}
        <p class={"help is-danger"}>This Email is invalid</p>
      {/if}
    </div>

    <label for="" class="label">Password</label>
    <span>
      <div class="control has-icons-left has-icons-right">
        <input
          type="password"
          class={password.length >= 8 ? "input is-success" : "input is-danger"}
          required
          bind:value={password}
        />
        <span class="icon is-small is-left">
          <i class="fas fa-lock" />
        </span>
        {#if password.length >= 8 && password !== "12345678"}
          <span class="icon has-text-success is-right">
            <i class="fas fa-check-square" />
          </span>
        {:else}
          <span class="icon has-text-danger is-right">
            <i class="fas fa-exclamation-triangle" />
          </span>
        {/if}
        <div>
          <span />
        </div>
        <div class="field" />
        <input
          type="submit"
          class="button is-fullwidth is-link"
          value="Enter Chat"
        />
      </div>
    </span>
  </div>
</form>
<hr />
<p class="has-text-centered">
  {#if mode === "signIn"}
    No Account? <br />
    <button class="button is-link" on:click={() => (mode = "signUp")}>
      Sign Up!</button
    >
  {:else}
    Already Signed up? <br />
    <button class="button is-link" on:click={() => (mode = "signIn")}>
      Log In!</button
    >
  {/if}
</p>
