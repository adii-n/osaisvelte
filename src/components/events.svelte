<script>
	import { Reload } from 'radix-icons-svelte';
	import { Button } from '@svelteuidev/core';	
	import { sleep } from '@svelteuidev/composables's ;
	import { Space, Text } from '@svelteuidev/core';

	let events = [];

	const getEventsFromAPI = async () => {
		const response = await fetch('https://api.opensourceatillinois.com/events');
		events = await response.json();
	};

	getEventsFromAPI()
	console.log(events)
	let clicked = false;
	
	
	function refreshAPI() {

		clicked = true;
		getEventsFromAPI();
		alert("API Refreshed");
		sleep(1000).then(() => {
			clicked = false;
		});
	}	
</script>

<div class="flex flex-row flex-wrap mx-auto justify-center font-XL m">   
<h1>All OSAI Events!</h1>
	<style>
		@font-face {
			font-family: 'Roboto';
			font-style: normal;
			font-weight: 400;
			src: local('Roboto'), local('Roboto'), url(https://fonts.gstatic.com/s/roboto/v20/KFOmCnqEu92Fr1Mu4mxKKTU1Kvnz.woff2) format('woff2');
			unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;

		}
		h1 {
			font-family: Roboto;
			font-size: 3em;
			font-weight: 400;
			color: #FFFFFF;
			text-align: center;
		}
	</style>

	

</div>

<div>
	<img class="titleimage" src="https://www.opensourceatillinois.com/_next/static/media/open-source.c5aedf9b.svg" alt="Event 1" width="300" height="300">

		<style>
			
			.titleimage {
				margin: 3rem;
				padding: 10px;
			}
			
		</style>

</div>



<div>
	
<Button class = "refreshbutton" on:click={refreshAPI}>
	{clicked ? "Refreshed API" : 'Refresh API'}
</Button>

<style>
	.refreshbutton {
		margin: 1rem;
		padding: 10px;
	}
</style>


</div>



<Space size="" />
	

<div class="flex flex-row flex-wrap mx-1 justify-center vertical-align: items-baseline mt-3">
	{#each events as event}
		<div class="flex w flex-col items-center bg-gray-300 p-5 m-5 d rounded-xl justify-between mt-3">
			<div class="text-lg font-bold text-center font-family Roboto bg-gray-300">
				{event.name}
				<style>
					div {
						font-family: Roboto;
						font-size: 1em;
						font-weight: 400;
						color: #000000;
						text-align: center;
					}

				</style>	
			</div>
			<div class ="bg-gray-300 text-center">
				{event.when}
				<style>
					div {
						font-family: Roboto;
						font-size: 1em;
						font-weight: 400;
						color: #000000;
						text-align: center;
					}

				</style>	

			</div>
		</div>
	{/each}
</div>