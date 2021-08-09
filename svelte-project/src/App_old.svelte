<script>
	import User from './User.svelte';
	let dataExists=false
	let id=null
	let promise1 = Promise.resolve([]);
	let promise2 = Promise.resolve([]);
	let disabled1=false
	
	
	async function fetchAllUsers() {
		const response = await self.fetch('https://jsonplaceholder.typicode.com/users');

		if (response.ok) {
  		return response.json();
			
		} else {
			throw new Error(users);
		}
	}

  function handleClick1() {
	disabled1=true
    promise1 = fetchAllUsers();
	}
	async function fetchUserById() {
		const response = await self.fetch(`https://jsonplaceholder.typicode.com/users/${id}`);

		if (response.ok) {
  		return response.json();
			
		} else {
			throw new Error(users);
		}
	}


	function handleClick2() {
	
    promise2 = fetchUserById();
	}

</script>

<main>
	<button on:click={handleClick1} disabled={disabled1} >Fetch Users</button>
	{#await promise1}
	<p>...waiting</p>
	{:then  users}
		{#each users as user}
			<User {...user}/>
		{/each}
	{/await}
	<br>
	<input type="number" placeholder="Enter Id" bind:value={id} required/>
	<input type="submit" on:click={handleClick2}  value="Find user with id"/>
	{#await promise2}
		<p>waiting...</p>
	{:then data}
		<User {...data}/>
	{/await}
	
	

</main>

<style>
	
	
</style>