<script>
	//https://jsonplaceholder.typicode.com/users //hit this

	//https://jsonplaceholder.typicode.com/users/${id} //hit by id

	import User from "./User.svelte";

	let userArray = [];
	let userData = null;
	async function getData() {
		let data = await fetch("https://jsonplaceholder.typicode.com/users");
		let response = await data.json();
		userArray = response;
	}

	async function getUser(id) {
		let data = await fetch(
			`https://jsonplaceholder.typicode.com/users/${id}`
		);
		let response = await data.json();
		userData = response;
	}
</script>

<button on:click={getData}>Fetch users</button>

<main>
	<div>
		<ul>
			{#each userArray as { id, name }}
				<li>
					<!-- getUser(user.id) -->
					<button on:click={() => getUser(id)}>
						Fetch {name}
					</button>
				</li>
			{/each}
		</ul>
	</div>

	{#if userData}
		<div>
			<User {...userData} />
		</div>
	{/if}
</main>

<style>
	main {
		display: flex;
	}
</style>
