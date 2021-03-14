<script>
  import { FirebaseApp, User } from "sveltefire";
  import firebase from "firebase/app";
  import "firebase/firestore";
  import "firebase/auth";
  import AuthForm from "./components/AuthForm.svelte";
  import SelectPage from "./components/SelectPage.svelte";

  const firebaseConfig = {
    apiKey: "AIzaSyA1I7m05hI0jhl3SJNZCYKUQ3IzbWGTfk0",
    authDomain: "mental-chat-eca48.firebaseapp.com",
    projectId: "mental-chat-eca48",
    storageBucket: "mental-chat-eca48.appspot.com",
    messagingSenderId: "111732300674",
    appId: "1:111732300674:web:43a655115f6895d9ee8d9b",
  };
  firebase.initializeApp(firebaseConfig);
</script>

<main class="app container section ">
  <FirebaseApp {firebase}>
    <User let:user let:auth>

      <SelectPage {user} />
      <button
        class="button is-fullwidth is-link"
        on:click={() => auth.signOut()}>Sign Out</button
      >

      <div slot="signed-out">
      <AuthForm {auth} />
      </div>
    </User>
  </FirebaseApp>
</main>

<style>
  .app {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    max-height: 100vh;
  }
</style>
