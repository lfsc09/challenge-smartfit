<script lang="ts">
	import required_mask from '$lib/resourses/images/required-mask.png';
	import recommended_mask from '$lib/resourses/images/recommended-mask.png';
	import required_towel from '$lib/resourses/images/required-towel.png';
	import recommended_towel from '$lib/resourses/images/recommended-towel.png';
	import partial_fountain from '$lib/resourses/images/partial-fountain.png';
	import not_allowed_fountain from '$lib/resourses/images/forbidden-fountain.png';
	import allowed_lockerroom from '$lib/resourses/images/required-lockerroom.png';
	import partial_lockerroom from '$lib/resourses/images/partial-lockerroom.png';
	import not_allowed_lockerroom from '$lib/resourses/images/forbidden-lockerroom.png';
</script>

<div class="legend-container">
	<div class="legend-item">
		<span class="legend-item-title">Máscara</span>
		<div class="legend-item-imgs">
			<div class="legend-item-img">
				<img src={required_mask} alt="Mascara" />
				<span>Obrigatório</span>
			</div>
			<div class="legend-item-img">
				<img src={recommended_mask} alt="Mascara" />
				<span>Recomendado</span>
			</div>
		</div>
	</div>
	<div class="legend-item">
		<span class="legend-item-title">Toalha</span>
		<div class="legend-item-imgs">
			<div class="legend-item-img">
				<img src={required_towel} alt="Mascara" />
				<span>Obrigatório</span>
			</div>
			<div class="legend-item-img">
				<img src={recommended_towel} alt="Mascara" />
				<span>Recomendado</span>
			</div>
		</div>
	</div>
	<div class="legend-item">
		<span class="legend-item-title">Bebedouro</span>
		<div class="legend-item-imgs">
			<div class="legend-item-img">
				<img src={partial_fountain} alt="Mascara" />
				<span>Parcial</span>
			</div>
			<div class="legend-item-img">
				<img src={not_allowed_fountain} alt="Mascara" />
				<span>Proibido</span>
			</div>
		</div>
	</div>
	<div class="legend-item">
		<span class="legend-item-title">Vestiários</span>
		<div class="legend-item-imgs">
			<div class="legend-item-img">
				<img src={allowed_lockerroom} alt="Mascara" />
				<span>Liberado</span>
			</div>
			<div class="legend-item-img">
				<img src={partial_lockerroom} alt="Mascara" />
				<span>Parcial</span>
			</div>
			<div class="legend-item-img">
				<img src={not_allowed_lockerroom} alt="Mascara" />
				<span>Proibido</span>
			</div>
		</div>
	</div>
</div>

<style>
	.legend-container {
		background-color: var(--very-light-grey);
		border-radius: 4px;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		gap: 16px;
		padding: 20px;
	}

	.legend-item {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 8px;

		& > .legend-item-title {
			font-weight: bold;
		}

		& > .legend-item-imgs {
			display: flex;
			flex-direction: row;
			gap: 8px;

			& > .legend-item-img {
				display: flex;
				flex-direction: column;
				align-items: center;

				& > img {
					height: 50px;
					width: 50px;
				}

				& > span {
					font-size: 15px;
				}
			}
		}
	}
</style>
