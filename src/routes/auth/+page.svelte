<script>
	// @ts-nocheck

	// import {setContext, getContext} from 'svelte';
	import { token } from '../../stores.js';
	import { redirect } from '@sveltejs/kit';
	// import { useNavigate, useLocation } from "@sveltejs/kit";
	import { goto } from '$app/navigation';
	// import { Router} from "@sveltejs/kit";

	//   const navigate = useNavigate();
	//   const location = useLocation();

	let loginUser = true;

	let email = '';
	let password = '';
	let error = '';

	// 	{
	//   "app_id": "string",
	//   "key_id": "string",
	//   "permissions": [
	//     "string"
	//   ],
	//   "redirect_uri": "string",
	//   "user_name": "string",
	//   "user_password": "string",
	//   "user_token": "string",
	//   "wallets": [
	//     "string"
	//   ]
	// }
	const getUserDetails = async (email, password) => {
		const res = await fetch('https://api.neucron.io/auth/login', {
			method: 'POST',
			body: JSON.stringify({
				app_id: '4fcf1801-664d-4c49-a7e0-914b45c75a99',
				key_id: 'Y2ZkNjA3',
				permissions: [],
				user_name: email,
				user_password: password,
				user_token: 'string',
			})
		});
		const body = await res.json();
		console.log(body);
		const statusCode = body.status_code;
		if (statusCode === 202) {
			// setContext(token, body.data )

			// console.log(getContext(token))
			console.log(token);
			// $token = body.data
			token.set(body.data);
			console.log(token);
			// const from = ($location.state && $location.state.from) || "/";
			// navigate(from, { replace: true });
			// redirect(200, '/mint')
			goto('/mint');
		} else {
			alert('Please try again');
		}

		// .then(res => {
		//     console.log(res.json().then((data) => console.log(data)))
		//     res.status === 202 ? setContext({"token": res.body.data }) : alert("error")
		//     console.log(getContext("token"))
		// });
	};

	async function login() {
		const user = await getUserDetails(email, password);
	}
	async function register() {
		const res = await fetch('https://api.neucron.io/auth/signup', {
			method: 'POST',
			body: JSON.stringify({ email, password })
		});
		//
		const body = await res.json();
		console.log(body);
		const statusCode = body.status_code;
		if (statusCode === 202) {
			// console.log(token)
			// $token = body.data
			token.set(body.data);
			// console.log(token)
			// const from = ($location.state && $location.state.from) || "/";
			// navigate(from, { replace: true });
			// redirect(200, '/mint')
			goto('/mint');
		} else {
			alert('Please try again');
		}
	}
	/*
    {
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2OTEwNTE0ODYsImlhdCI6MTY4ODQ1OTQ4NiwiaXNzIjoiaHR0cHM6Ly9uZXVjcm9uLmlvIiwianRpIjoiMjJkYzlkZTMtNjlkNi00MTM3LWE5YjItZjExNTRkZjY2NjMyIiwibmJmIjoxNjg4NDU5NDg2LCJzdWIiOiJiOWRhMmEzYi02OTc2LTRlMzMtOTIxNC05YmMwNTRkYTAwOGYiLCJ1c2VyX2lkIjoiYjlkYTJhM2ItNjk3Ni00ZTMzLTkyMTQtOWJjMDU0ZGEwMDhmIn0.MmBmBwAYa73X1qeww5xh5li2bMQQtMycCIQoyNqO5Ak",
    "user_id": "b9da2a3b-6976-4e33-9214-9bc054da008f"
}
*/
</script>

<!-- <Router> -->

<section
	class="flex items-center justify-center w-full bg-gradient-to-b from-[#141943] via-[#141943] to-[#3c0f5e] h-[90vh] relative px-12 overflow-clip"
>
	<div class="absolute z-0 xl:-right-20 right-0">
		<img src="/images/PinkArt.png" class="" alt="anokha design" />
	</div>
	<div class="absolute z-0 xl:top-[70%] top-10 hidden xl:block">
		<img src="/images/GreenArt.png" alt="anokha design" />
	</div>
	<div class="absolute z-0 xl:-left-20 hidden xl:block left-0">
		<img src="/images/GreyArt.png" alt="anokha design" />
	</div>

	<div class="w-full flex justify-center">
		{#if loginUser}
			<form
				on:submit|preventDefault={login}
				class="backdrop flex flex-col col-6 bg-gradient-to-b from-transparent to-[#ffffff2e] p-[60px] border border-[#FFFFFF4D] z-20 rounded-xl xl:mx-0 items-center"
			>
				<div class="w-ful">
					<h1 class="text-6xl text-white mb-10">Login</h1>
					<div class="mb-6 flex flex-col">
						<label for="email" class="text-[#27EE52] text-base pb-2">Email</label>
						<input
							type="email"
							class="bg-transparent text-white border-b border-[#27EE52] outline-none"
							id="email"
							placeholder="username@email.com"
							bind:value={email}
						/>
					</div>

					<div class="mb-3 flex-col flex">
						<label for="password" class="text-[#27EE52] text-base pb-2">Password</label>
						<input
							type="password"
							class="bg-transparent text-white border-b border-[#27EE52] outline-none"
							placeholder="******"
							id="password"
							bind:value={password}
						/>
					</div>

					<button
						type="submit"
						class="text-2xl text-white bg-green-500 rounded-3xl w-full mt-5 py-1 px-3"
						>Submit</button
					>
					<div id="error_message" class="text-danger">
						<!-- <small>{error}</small> -->
					</div>
					<div class="flex mt-4">
						<p class="text-sm text-white">
							Dont have an account ? <button
								on:click={() => {
									loginUser = false;
								}}
								class="text-sm mt-3 text-white underline rounded-lg py-1 px-1"
								>Register for free</button
							>
						</p>
					</div>
				</div>
			</form>
		{:else}
			<form
				on:submit|preventDefault={register}
				class="backdrop flex flex-col col-6 bg-gradient-to-b from-transparent to-[#ffffff2e] p-[82px] py-[60px] border border-[#FFFFFF4D] z-20 rounded-xl xl:mx-0 items-center"
			>
				<div class="w-ful">
					<h1 class="text-6xl text-white mb-10">Register</h1>
					<div class="mb-6 flex flex-col">
						<label for="email" class="text-[#27EE52] text-base pb-2">Email</label>
						<input
							type="email"
							class="bg-transparent text-white border-b border-[#27EE52] outline-none"
							id="email"
							placeholder="username@email.com"
							bind:value={email}
						/>
					</div>

					<div class="mb-3 flex-col flex">
						<label for="password" class="text-[#27EE52] text-base pb-2">Password</label>
						<input
							type="password"
							class="bg-transparent text-white border-b border-[#27EE52] outline-none"
							placeholder="******"
							id="password"
							bind:value={password}
						/>
					</div>

					<button
						type="submit"
						class="text-2xl text-white bg-green-500 rounded-3xl w-full mt-5 py-1 px-3"
						>Submit</button
					>
					<div id="error_message" class="text-danger">
						<!-- <small>{error}</small> -->
					</div>
					<div class="flex mt-4">
						<p class="text-sm text-white">
							Have an account already? <button
								on:click={() => {
									loginUser = true;
								}}
								class="text-sm mt-3 text-white underline rounded-lg py-1 px-1">Login here</button
							>
						</p>
					</div>
				</div>
			</form>
		{/if}
	</div>
</section>

<!-- </Router> -->
<style>
	.backdrop {
		backdrop-filter: blur(12px);
	}
</style>
