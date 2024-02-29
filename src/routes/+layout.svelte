<script lang="ts">
	import './styles.css';
	import logo from '$lib/resourses/images/logo.svg';
</script>

<div class="app">
	<header>
		<img src={logo} alt="Logo" />
	</header>

	<slot />

	<footer>
		<img src={logo} alt="Logo" />
		<p>Todos os direitos reservados - 2020</p>
	</footer>
</div>

<style>
	.app {
		height: 100%;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: center;

		& > header {
			width: 100%;
			display: flex;
			flex-direction: row;
			justify-content: center;
			align-items: center;
			background-color: black;
			padding: 16px;

			& > img {
				height: 80px;
				width: 150px;
			}
		}

		& > footer {
			width: 100%;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			background-color: var(--dark-grey);
			padding: 32px;

			& > img {
				height: 40px;
				width: 100px;
			}

			& > p {
				color: white;
				font-size: 14px;
			}
		}
	}
</style>
