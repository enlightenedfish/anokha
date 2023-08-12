<script>
	// import { page } from '$app/stores';

	// Function to toggle header menu in mobile view.
	// function toggleMenu(flag) {
	//     let value = document.getElementById("menu");
	//     if (flag) {
	//         value.classList.remove("hidden");
	//     } else {
	//         value.classList.add("hidden");
	//     }
	// }
	// import { get } from 'svelte/store';

	export let user;
	export let isLoggedIn = false;
	// import {session} from '$app/stores';
	// const sessionObject = get(session);
	// console.log("session is giving user as " + JSON.stringify(user))
	// console.log("session is giving user as " + JSON.stringify(user))
	console.log("isLoggedIn" + isLoggedIn)


	//   import authStore from '$lib/stores/authStore';
	//   import firebase from 'firebase/app';
	// //   let isOpen = false;
	// handles the logout of
	//   async function logout() {
	//     await firebase.auth().signOut();
	//   }
	import { goto } from '$app/navigation';

	import ConnectWallet from '$lib/connectNeucron.svelte';
	// import Profile from '$lib/components/header/profile.svelte';

	// import { logOut } from '$lib/client/firebase';
	// const links = [
	// 	['Create Gift', 'createGift'],
	// 	['My NFTs', 'mynfts']
	// ];


</script>

<div class="sticky top-0 z-30 max-w-screen-lg pl-5 mx-auto mt-10 lg:pl-10 backdrop-filter backdrop-blur-lg bg-opacity-20 navbar">
	<div class="flex-1">

		<div aria-label="Home. logo" role="img">
			<a href="/">
				<img class="md:w-auto" src="/icons/NFTYGiftz.svg" alt="NftyGiftz" />
			</a>
		</div>
	</div>

	{#if isLoggedIn}

	<div class="flex-none">
		<div class="dropdown dropdown-end">
				<div class="mx-2 indicator">
					<button aria-label="show notifications" class="relative flex items-center justify-center h-full cursor-pointer btn btn-ghost btn-circle focus:outline-none hover:text-indigo-100 focus:text-indigo-100 text-indigo-50">
						<svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-bell" width="28" height="28" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round">
							<path stroke="none" d="M0 0h24v24H0z" />
							<path d="M10 5a2 2 0 0 1 4 0a7 7 0 0 1 4 6v3a4 4 0 0 0 2 3h-16a4 4 0 0 0 2 -3v-3a7 7 0 0 1 4 -6" />
							<path d="M9 17v1a3 3 0 0 0 6 0v-1" />
						</svg>
						<div class="absolute top-0 pt-1 pr-1 mt-0 mr-4 left-4">
							<div class="w-2 h-2 bg-red-400 rounded-full"></div>
						</div>
						<div class="absolute bottom-0 pb-2 pl-1 mb-0 ml-4 right-3">
							<span class="badge badge-sm indicator-item">0</span>
						</div>
					</button>

				</div>

			<div tabindex="0" class="mt-3 shadow card card-compact w-52 dropdown-content bg-base-100">
				<div class="card-body">
					<span class="text-lg font-bold">You have</span>
					<span class="text-info">Received an NFT</span>
					<div class="card-actions">
						<button class="btn btn-primary btn-block">View NFT</button>
					</div>
				</div>
			</div>
		</div>
		
		<div class="dropdown dropdown-end">
			<label tabindex="0" class="btn btn-ghost btn-circle avatar">
				<div class="w-10 rounded-full">
					<img src={user.avatarUrl} />
				</div>
			</label>
			<ul
				tabindex="0"
				class="p-2 mt-3 shadow menu menu-compact dropdown-content bg-base-100 rounded-box w-52"
			>
				<li> Welcome {user.displayName}</li>

				<li>
					<a sveltekit:prefetch href="/mynfts" class="justify-between">
						My NFTs
						<span class="badge">New</span>
					</a>
				</li>
				<!-- <li><a sveltekit:prefetch href="/giftroom">Gift ShowRoom</a></li> -->
				<!-- <li><a sveltekit:prefetch href="/createGift">Send Gift</a></li> -->
				<!-- <li><a sveltekit:prefetch href="/sendGift">Send Gift</a></li> -->
				<!-- <li><a sveltekit:prefetch href="/preferences">Preferences</a></li>
				<li><a sveltekit:prefetch href="/profile">Artist Profile</a></li> -->
				<button on:click={()=>goto('/handcash/logout')} class="px-1 py-1 mt-3 text-sm transition duration-150 ease-in-out border border-white bg-opacity-70 bg-accent-focus ring-white focus:outline-none lg:text-lg lg:font-bold focus:ring-2 focus:ring-offset-2 focus:ring-tertiary md:block hover:text-accent-focus hover:bg-white rounded-2xl sm:px-8 sm:py-3">Logout</button>
			</ul>
		</div>

	</div>

	{:else}
        <ConnectWallet />
<!-- <button on:click={()=>{goto('/login')}} class="hidden px-4 py-1 text-sm transition duration-150 ease-in-out bg-transparent bg-indigo-600 border border-white ring-white focus:outline-none lg:text-lg lg:font-bold focus:ring-2 focus:ring-offset-2 focus:ring-indigo-700 md:block hover:text-indigo-600 hover:bg-white rounded-2xl sm:px-8 sm:py-3">Login</button> -->

{/if}

</div>


<style>
	.active {
		text-decoration: underline;
	}
</style>
