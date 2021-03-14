<script>
  import Chats from "./Chats.svelte";
  export let user;
  user.mode = '';
</script>

{#if user.mode === ''}
<h1 class="title has-text-info has-text-centered">Select Chat Room</h1>
<div class="buttons">
  <button on:click={() => {user.mode = "depression"}} class=" selected button is-light is-link is-medium " type="submit">Depression</button>
  <button on:click={() => {user.mode = "Schizophrenia"}} class=" selected button is-light is-link is-medium " type="submit">Schizophrenia</button>
  <button on:click={() => {user.mode = "personality "}} class=" selected button is-light is-link is-medium " type="submit">Personality Disorders</button>
  <button on:click={() => {user.mode = "ADD"}} class=" selected button is-light is-link is-medium " type="submit">ADD</button>
  <button on:click={() => {user.mode = "sleep"}} class=" selected button is-light is-link is-medium " type="submit">Sleep Wake Disorders</button>
  <button on:click={() => {user.mode = "eating"}} class=" selected button is-light is-link is-medium " type="submit">Eating Disorders</button>
  <button on:click={() => {user.mode = "OCD"}} class=" selected button is-light is-link is-medium " type="submit">OCD</button>
  <button on:click={() => {user.mode = "ADHD"}} class=" selected button is-light is-link is-medium " type="submit">ADHD</button>
  <button on:click={() => {user.mode = "autisim"}} class=" selected button is-light is-link is-medium " type="submit">Autisim</button>
  <button on:click={() => {user.mode = "Associative"}} class=" selected button is-light is-link is-medium " type="submit">Associative Disorders</button>
</div>
{:else}
<Chats {user}/>
{/if}
