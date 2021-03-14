<script>
import App from "../App.svelte";

  export let auth;
  let mode = "signIn";
  let email = "";
  let password = "";
  let homepg=true;
  async function handleSubmit() {
    if (mode === "signIn") {
      await auth.signInWithEmailAndPassword(email, password);
    } else {
      await auth.createUserWithEmailAndPassword(email, password);
      email = "";
      password = "";
    }
  }
</script>
<body>
<h1 class="title has-text-info has-text-centered">Mental Health Chat</h1>
{#if homepg == true}

<p style="padding-top:20%"class="has-text-centered">
 
<button class="button is-link is-large" on:click={() => (homepg = false)}>
  Sign In</button
>

</p>
<p  style="padding-top:7px" class="has-text-centered">
  Don't have an account?
  <span style="cursor: pointer" class=" has-text-link link" on:click={() => (mode = 'signUp', homepg=false)}>Sign Up</span>
</p>
<div style="padding-left:31%; padding-top:27%"class="container">
<p style="width:50%; " class="has-text-centered">
  At mental health chat we strive to help the younger generation deal with their mental health issues thorugh an online group therapy type of approach. Mental Health Chat allows the users to connect with other users with similar issue and talk about them anonymously.
</p><br/>
<p style="width: 50%" class="has-text-centered"><small></small>If you are having suicidal thoughts or actions, please call <span class="has-text-info">1-800-273-8255</span><small></small></p>
</div>
{:else}


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
{/if}
</body>