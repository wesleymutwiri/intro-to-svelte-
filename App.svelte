<script>
import { onMount } from "svelte";
import User from "./User.svelte";
let users;

onMount(() => {
  getGithubUsers();
});

function getGithubUsers() {
  fetch("https://api.github.com/users")
  .then(resp => resp.json())
  .then(data => (users = data));
}
</script>

<style>
 
</style>

<main>
  <h1> This is something</h1>
{#if users}
<ul>
{#each users as user}
<li> 
<User username={user.login} avatar={user.avatar_url}/>
</li>
{/each}
</ul>    
{/if}
{users}
</main>