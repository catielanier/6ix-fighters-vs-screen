<script>
  import { setToken } from "../utils/tokenService";
  import { getAuth, signInWithEmailAndPassword } from "firebase/auth";
  import { firebase } from "../utils/firebase";
  export let setLogin;
  let email = "";
  let password = "";

  const submitLogin = async (e) => {
    e.preventDefault();
    const auth = getAuth(firebase);
    signInWithEmailAndPassword(auth, email, password).then((user) => {
      setToken(JSON.stringify(user));
      setLogin();
    });
  };
</script>

<div class="login">
  <form on:submit={submitLogin}>
    <input type="email" bind:value={email} placeholder="Email address" />
    <input type="password" bind:value={password} placeholder="Password" />
    <button type="submit">Login</button>
  </form>
</div>
