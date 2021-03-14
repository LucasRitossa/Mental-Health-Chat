<script>
  import { Collection } from "sveltefire";
  import {tick} from "svelte"
  import AppendMessage from "./AppendMessage.svelte";
  export let user;

let chatsElement
async function scrollToTheEnd() {
  await tick()
  chatsElement.scrollTo(0,chatsElement.scrollHeight)
}
</script>
<style>
  .chat-box {
    flex: 1;
    display: flex;
    flex-direction: column;
    overflow-y: auto;
  }
  .is-reciever {
    text-align: left;
    margin-right: auto;
  }
  .is-sender {
    text-align: right;
    margin-left: auto;
  }
</style>

<Collection
  path={`/${user.mode}`}
  let:ref={chatsRef}
  let:data={messages}
  on:data={scrollToTheEnd}
>
  <div class="box chat-box" bind:this={chatsElement}>
    {#each messages.sort((a, b) => a.date - b.date) as { message, uid }}
      <div style={uid === user.uid ? 'margin-left:auto' : 'margin-right:auto'} class="tag is-light">{uid}</div>
      <div
        class="notification {uid === user.uid
          ? 'is-info is-sender'
          : 'is-success is-reciever'}"
      >
        {message}
      </div>
    {/each}
  </div>
  <AppendMessage {chatsRef} {user} />
</Collection>

