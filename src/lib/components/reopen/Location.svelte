<script lang="ts">
	import type { TypeLocation } from '../../../routes/+page.svelte';

	/*********
	 * PARAMS
	 **********/
	export let data: TypeLocation;
</script>

<div class="location-item">
	<span class="location-item-status" class:open={data.opened} class:closed={!data.opened}
		>{data.opened ? 'Aberto' : 'Fechado'}</span
	>
	<h3 class="location-item-title">{data.title}</h3>
	<span class="location-item-content">{@html data.content}</span>
	<hr />
</div>

<style>
	.location-item {
		background-color: var(--very-light-grey);
		padding: 16px;
		border-radius: 4px;

		& > .location-item-status {
			font-weight: 600;

			&.open {
				color: var(--green);
			}

			&.closed {
				color: var(--red);
			}
		}
	}

	.location-item-title {
		color: var(--dark-grey);
	}

	.location-item-content {
		color: var(--light-grey);
		font-size: 14px;
	}
</style>
