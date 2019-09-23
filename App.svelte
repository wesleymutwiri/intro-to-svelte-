<script>
import { onMount } from "svelte";
import User from "./User.svelte";
import UserSearch from './UserSearch.svelte';
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
 .user-list {
   display: flex;
   flex-flow: wrap;
   list-style: none;
   margin: 0;
   padding: 0;

 }

 .user-list li {
   width: 20%;
   padding: 10px;
 }
</style>

<main>
  <UserSearch/>
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