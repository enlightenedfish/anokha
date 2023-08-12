<script>
	import { page } from '$app/stores';
	import { token } from '../stores.js';
</script>

<header class="bg-[#141943] pt-4 flex xl:justify-around justify-between items-center gap-3">
	<div aria-current={$page.url.pathname === '/' ? 'page' : undefined} class="max-w-[40%] mt-2">
		<a href="/"><img src="/images/anokha.png" alt="" /></a>
	</div>

	<nav>
		<ul
			class={`hidden xl:flex mt-3 justify-center gap-5 bg-transparent text-white xl:text-3xl font-bold ${
				$token ? '' : 'xl:hidden'
			} `}
		>
			<li aria-current={$page.url.pathname === '/mint' ? 'page' : undefined}>
				<a
					href="/mint"
					class="hover:underline underline-offset-8 hover:decoration-[#70E5FE] focus:underline"
					>Create</a
				>
			</li>
			<li aria-current={$page.url.pathname.startsWith('/mynfts') ? 'page' : undefined}>
				<a
					href="/mynfts"
					class="hover:underline underline-offset-8 hover:decoration-[#70E5FE] focus:underline"
					>Collection</a
				>
			</li>
		</ul>
	</nav>
	<div class={`flex gap-3 `}>
		<div class={`${$token ? '' : 'hidden'} group relative xl:hidden `}>
			<button class="px-4 py-2 border border-emerald-500 text-emerald-500 h-full"> Explore </button>
			<div class="hidden group-focus-within:block absolute bg-green-400 p-5 w-fit rounded z-20">
				<ul>
					<li aria-current={$page.url.pathname === '/mint' ? 'page' : undefined}>
						<a
							href="/mint"
							class="hover:underline underline-offset-8 hover:decoration-[#70E5FE] focus:underline"
							>Create</a
						>
					</li>
					<li aria-current={$page.url.pathname.startsWith('/mynfts') ? 'page' : undefined}>
						<a
							href="/mynfts"
							class="hover:underline underline-offset-8 hover:decoration-[#70E5FE] focus:underline"
							>Collection</a
						>
					</li>
				</ul>
			</div>
		</div>
		<a href="/auth">
			<button class={`${$token ? 'hidden' : ''} px-5 py-3 rounded bg-[#70E5FE] `}> Sign Up </button>
			<button
				class={`${$token ? '' : 'hidden'} px-5 py-3 rounded bg-[#70E5FE] `}
				on:click={() => {
					$token = null;
				}}
			>
				Sign Out
			</button>
		</a>
	</div>
</header>

<style>
</style>
