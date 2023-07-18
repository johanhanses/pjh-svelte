<script lang="ts">
	import { enhance } from '$app/forms'
	import { navigating } from '$app/stores'
	import type { ActionData } from './$types'

	export let form: ActionData
	let loading = false
</script>

<form
	action="?/login"
	method="POST"
	use:enhance={() => {
		loading = true
		return async ({ update }) => {
			await update()
			loading = false
		}
	}}
>
	<div class="max-w-sm space-y-4 mx-auto">
		<div>
			<label for="username" class="sr-only">Username</label>
			<input
				id="username"
				name="username"
				type="text"
				required
				placeholder="Username"
				class="border p-2 placeholder:text-sm w-full"
			/>
		</div>

		<div>
			<label for="password" class="sr-only"> Password </label>
			<input
				name="password"
				type="password"
				required
				placeholder="Password"
				class="border p-2 placeholder:text-sm w-full"
			/>
		</div>

		<button type="submit" class="border p-2 w-full">
			{#if loading || $navigating}
				<span>loading...</span>
			{:else}
				<span>Log in</span>
			{/if}
		</button>

		{#if form?.invalid}
			<p class="text-red-500">Username and password is required.</p>
		{/if}

		{#if form?.credentials}
			<p class="text-red-500">You have entered the wrong credentials.</p>
		{/if}
	</div>
</form>
