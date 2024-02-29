<script lang="ts" context="module">
	type TypeLocation = {
		content: string;
		fountain: 'partial' | 'not_allowed';
		id: string;
		locker_room: 'allowed' | 'partial' | 'not_allowed';
		mask: 'required' | 'recommended';
		opened: boolean;
		schedules: {
			weekdays: 'Seg. à Sex.' | 'Sáb.' | 'Dom.';
			hour: string;
		}[];
		title: string;
		towel: 'required' | 'recommended';
	};

	export type { TypeLocation };
</script>

<script lang="ts">
	import Forms from '$lib/components/reopen/Forms.svelte';
	import Legend from '$lib/components/reopen/Legend.svelte';
	import Location from '$lib/components/reopen/Location.svelte';
	import cloneDeep from 'lodash.clonedeep';
	import { onMount } from 'svelte';

	/*******
	 * VARS
	 ********/
	let locations: undefined | TypeLocation[] = undefined;
	let filtered_locations: undefined | TypeLocation[] = undefined;

	/********
	 * FUNCS
	 *********/
	onMount(() => {
		fetch('https://test-frontend-developer.s3.amazonaws.com/data/locations.json')
			.then((response) => response.json())
			.then((values) => {
				let treated_locations: any = {};
				let location: TypeLocation;
				for (location of values.locations) {
					if (!(location.id in treated_locations)) treated_locations[location.id] = location;
				}
				locations = cloneDeep(Object.values(treated_locations));
				console.log(locations);
				filtered_locations = cloneDeep(locations);
			})
			.catch((err) => {
				locations = undefined;
			});
	});
</script>

<main>
	<section class="reopen-title">
		<h1>Reabertura <br />Smart Fit</h1>
		<div class="separator" />
		<p>
			O horário de funcionamento das nossas unidades está seguindo os decretos de cada município.
			Por isso, confira aqui se a sua unidade está aberta e as medidas de segurança que estamos
			seguindo.
		</p>
	</section>
	<section class="reopen-forms">
		<Forms {locations} bind:filtered_locations />
	</section>
	<section class="reopen-legend">
		<Legend />
	</section>
	<section class="reopen-locations">
		{#if filtered_locations && filtered_locations.length > 0}
			<div class="reopen-locations-container">
				{#each filtered_locations as location (location.id)}
					<Location data={location} />
				{/each}
			</div>
		{:else}
			<div class="reopen-locations-empty">Nenhuma unidade encontrada</div>
		{/if}
	</section>
</main>

<style>
	main {
		height: 100%;
		padding: 48px 10% 48px 10%;
		display: flex;
		flex-direction: column;
		gap: 32px;

		& > .reopen-title {
			& > h1 {
				font-size: 32px;
				text-transform: uppercase;
				margin: 16px 0 16px 0;
			}

			& > .separator {
				height: 8px;
				width: 75px;
				background-color: var(--dark-grey);
			}

			& > p {
				margin: 32px 0 0 0;
				line-height: 24px;
			}
		}

		& > .reopen-locations {
			& > .reopen-locations-container {
				display: grid;
				gap: 16px;
				grid-template-columns: repeat(3, 1fr);
				grid-auto-rows: minmax(100px, auto);
			}

			& > .reopen-locations-empty {
				display: flex;
				flex-direction: row;
				justify-content: center;
				align-items: center;
				font-size: 26px;
				color: var(--light-grey);
				text-transform: uppercase;
				border: solid 2px var(--very-light-grey);
				border-radius: 4px;
				padding: 32px;
			}
		}
	}
</style>
