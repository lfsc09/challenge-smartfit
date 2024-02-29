<script lang="ts">
	import clock_icon from '$lib/resourses/images/icon-hour.png';
	import { onMount } from 'svelte';
	import type { TypeLocation } from '../../../routes/+page.svelte';
	import cloneDeep from 'lodash.clonedeep';

	/********
	 * TYPES
	 *********/
	type TypeFilterData = {
		period: '06:00 até 12:00' | '12:01 até 18:00' | '18:01 até 23:00' | '';
		show_closed_locations: boolean;
	};

	/*********
	 * PARAMS
	 **********/
	export let locations: TypeLocation[] | undefined;
	export let filtered_locations: TypeLocation[] | undefined;

	/*******
	 * VARS
	 *******/
	let form__filter_data: TypeFilterData = {
		period: '',
		show_closed_locations: false
	};

	/********
	 * FUNCS
	 *********/
	const handle_periodChange = (event: any) => {
		form__filter_data.period = event.currentTarget.value;
	};

	const handle_filter = () => {};

	const handle_clear = () => {
		filtered_locations = cloneDeep(locations);
		form__filter_data = {
			period: '',
			show_closed_locations: false
		};
	};

	$: console.log(form__filter_data);
</script>

<div class="forms-container">
	<div class="forms-container-title">
		<img src={clock_icon} alt="Clock Image" />
		<span>Horário</span>
	</div>
	<div class="forms-fields">
		<h3 class="forms-fields-title">Qual período quer treinar?</h3>
		<div class="separator" />
		<form>
			<div>
				<div class="period">
					<div>
						<input
							type="radio"
							value="06:00 até 12:00"
							name="period"
							id="period_morning"
							checked={form__filter_data.period === '06:00 até 12:00'}
							on:change={handle_periodChange}
						/>
						<label for="period_morning">Manhã</label>
					</div>
					<span>06:00 às 12:00</span>
				</div>
				<div class="period">
					<div>
						<input
							type="radio"
							value="12:01 até 18:00"
							name="period"
							id="period_afternoon"
							checked={form__filter_data.period === '12:01 até 18:00'}
							on:change={handle_periodChange}
						/>
						<label for="period_afternoon">Tarde</label>
					</div>
					<span>12:01 às 18:00</span>
				</div>
				<div class="period">
					<div>
						<input
							type="radio"
							value="18:01 até 23:00"
							name="period"
							id="period_night"
							checked={form__filter_data.period === '18:01 até 23:00'}
							on:change={handle_periodChange}
						/>
						<label for="period_night">Noite</label>
					</div>
					<span>18:01 às 23:00</span>
				</div>
			</div>
			<div>
				<div class="show-closed-locations">
					<input
						type="checkbox"
						id="show_closed_locations"
						bind:checked={form__filter_data.show_closed_locations}
					/>
					<label for="show_closed_locations">Exibir unidades fechadas</label>
				</div>
				<div class="filtered-results">
					<span>Resultados encontrados:</span>
					<span>{filtered_locations?.length ?? 0}</span>
				</div>
			</div>
		</form>
	</div>
	<div class="forms-actions">
		<button type="button" class="forms-actions-send" on:click={handle_filter}
			>Encontrar Unidade</button
		>
		<button type="button" class="forms-actions-clear" on:click={handle_clear}>Limpar</button>
	</div>
</div>

<style>
	.forms-container {
		border: solid 2px var(--very-light-grey);
		padding: 12px;
		border-radius: 4px;
	}

	.forms-container-title {
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: 10px;

		& > img {
			height: 25px;
		}

		& > span {
			color: var(--light-grey);
		}
	}

	.forms-fields {
		& > .forms-fields-title {
			color: var(--light-grey);
			font-size: 22px;
			font-weight: 500;
			margin-bottom: 14px;
		}

		& > .separator {
			width: 100%;
			height: 1px;
			background-color: var(--light-grey);
		}

		& > form {
			margin-top: 16px;
			color: var(--light-grey);

			& > div:first-child {
				display: flex;
				flex-direction: column;
				gap: 8px;

				& > .period {
					line-height: 20px;
					padding: 6px 0 6px 0;
					border-bottom: 1px solid var(--light-grey);
					display: flex;
					flex-direction: row;
					justify-content: space-between;
				}
			}

			& > div:last-child {
				display: flex;
				flex-direction: row;
				justify-content: space-between;
				align-items: center;
				line-height: 28px;
				margin-top: 32px;
				color: initial;

				& > .show-closed-locations {
					& > label {
						user-select: none;
					}
				}

				& > .filtered-results {
					display: flex;
					flex-direction: row;
					align-items: center;
					gap: 4px;

					& > span:nth-child(2) {
						font-size: 20px;
						font-weight: bold;
					}
				}
			}
		}
	}

	.forms-actions {
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		gap: 16px;
		padding: 24px 0 8px 0;

		& > button {
			font-weight: bold;
			text-transform: uppercase;
			padding: 8px 0 8px 0;
			width: 30%;
			border-radius: 2px;
			cursor: pointer;
		}

		& > .forms-actions-send {
			background-color: var(--yellow);
			border: 1px solid var(--very-light-grey);
		}

		& > .forms-actions-clear {
			background-color: white;
			border: 1px solid var(--light-grey);
		}
	}
</style>
