<script lang="ts">
	import data from '../../../data/web-design';
	import placeholder from '../../../actions/placeholder';

	const chunk = (arr: any[], columnCount: number): any[][] =>
		Array.from({ length: columnCount }, (_v, arrayIndex) => {
			return arr.filter((_it, itemIndex) => itemIndex % columnCount === arrayIndex);
		});

	let columns = chunk(Object.entries(data), 3);
	let clientWidth = Infinity;

	$: columns = chunk(Object.entries(data), clientWidth >= 1200 ? 3 : clientWidth >= 768 ? 2 : 1);
</script>

<svelte:window bind:innerWidth={clientWidth} />

<h2 class="design-title">Web Design</h2>

<section class="design-main">
	<div class="masonry">
		{#each columns as cards}
			<div class="column">
				{#each cards as [_id, card]}
					<a class="card" href={card.href}>
						<img class="card-image" use:placeholder src={card.img} alt={card.alt} />
						<div class="card-main">
							<h3 class="card-title">{card.title}</h3>
							<p class="card-subtitle">{card.subtitle}</p>
							<p class="card-description">{card.description}</p>
						</div>
					</a>
				{/each}
			</div>
		{/each}
	</div>
</section>

<style>
	.masonry {
		display: flex;
		justify-content: center;
	}

	.column {
		display: flex;
		flex-flow: column;
	}

	.card {
		box-shadow: 2px 2px 4px 0px #0a0a0a80;
		border: 1px solid rgba(10, 10, 10, 0.3);
		border-top: 5px solid var(--black);
		margin: 0.5rem;
		margin-top: 0;
		margin-bottom: 1rem;
		display: flex;
		flex-direction: column;
		height: min-content;
		cursor: pointer;
		min-width: 20ch;
		max-width: 40ch;
		text-decoration: none;
	}

	.card-image {
		max-width: 100%;
		height: auto;
		margin: max(1rem, 1.2vw);
	}

	.card-main {
		margin: max(1rem, 1.2vw);
		margin-top: 0;
	}

	.card-title {
		font-family: 'Lalezar', cursive;
		font-weight: 400;
		color: var(--white);
		--val: 2vw;
		--min: 1.8em;
	}

	.card-subtitle {
		font-family: 'Open Sans', sans-serif;
		font-weight: 300;
		color: var(--light-gray);
		--val: 0.2vw;
		--min: 0.7em;
		margin-top: max(0.5rem, 0.5vw);
		margin-bottom: max(1rem, 1vw);
	}

	.card-description {
		font-family: 'Open Sans', sans-serif;
		font-weight: 300;
		color: var(--white);
		--val: 1vw;
		--min: 0.9em;
	}
</style>
