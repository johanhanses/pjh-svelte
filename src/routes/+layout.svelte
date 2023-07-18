<script lang="ts">
	import { enhance } from '$app/forms'
	import { page } from '$app/stores'
	import '../app.css'
</script>

<svelte:head>
	<title>Pjh</title>
</svelte:head>

<nav class="bg-stone-800 text-white p-8 font-serif flex space-x-6">
	{#if !$page.data.user}
		<a href="/login">Login</a>
		<a href="/register">Register</a>
	{/if}

	{#if $page.data.user}
		<a href="/admin">Admin</a>

		<form class="logout" action="/logout" method="POST" use:enhance>
			<button type="submit">Log out</button>
		</form>
	{/if}
</nav>

<main class="p-8">
	<slot />
</main>
