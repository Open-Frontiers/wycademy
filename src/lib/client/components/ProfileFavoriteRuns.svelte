<script lang="ts">
	import ClickableTileImage from './ClickableTileImage.svelte';
	import FavoriteFilled from 'carbon-icons-svelte/lib/FavoriteFilled.svelte';
	import Favorite from 'carbon-icons-svelte/lib/Favorite.svelte';
	import { monsterInfo } from '../modules/frontier/monsters';
	import MonsterComponent from './frontier/icon/dynamic-import/MonsterComponent.svelte';

	interface Props {
		favoriteRuns?: any;
	}

	let {
		favoriteRuns = [
			{
				displayName: 'Burning Freezing Elzelion',
				title: "User 2's Run #130",
				link: '/',
				totalFavorites: 0,
			},
			{
				displayName: 'Conquest Crimson Fatalis',
				title: "User 2's Run #131",
				link: '/',
				totalFavorites: 0,
			},
			{
				displayName: 'Supremacy Pariapuria',
				title: "User 3's Run #132",
				link: '/',
				totalFavorites: 0,
			},
			{
				displayName: 'Bombardier Bogabadorumu',
				title: "User 4's Run #133",
				link: '/',
				totalFavorites: 0,
			},
			{
				displayName: 'Ruling Guanzorumu',
				title: "User 5's Run #134",
				link: '/',
				totalFavorites: 0,
			},
			{
				displayName: 'Zenith Espinas',
				title: "User 6's Run #135",
				link: '/',
				totalFavorites: 0,
			},
			{
				displayName: 'Zenith Espinas',
				title: "User 7's Run #136",
				link: '/',
				totalFavorites: 0,
			},
			{
				displayName: 'Conquest Fatalis',
				title: "User 8's Run #130",
				link: '/',
				totalFavorites: 0,
			},
		],
	}: Props = $props();

	const maxFavoritesToDisplay = 5;

	const displayedFavorites = Object.values(favoriteRuns).slice(
		0,
		maxFavoritesToDisplay,
	);
</script>

<div class="container">
	{#each displayedFavorites as favoriteRun}
		<a class="run-container" href={favoriteRun.link}>
			<div class="icon">
				{#if monsterInfo.find((e) => e.displayName === favoriteRun.displayName)?.unusedComponent === true}
					<img
						src={monsterInfo.find(
							(e) => e.displayName === favoriteRun.displayName,
						)?.icon}
						width="64"
						alt="Favorite Icon"
					/>
				{:else}
					<MonsterComponent
						currentMonster={favoriteRun.displayName}
						size="64px"
					/>
				{/if}
			</div>
			<div class="text">
				<p class="title">
					{favoriteRun.title}
				</p>
				<div class="total-favorites-count">
					<div>
						<FavoriteFilled
							title="Favorited by {favoriteRun.totalFavorites} users"
							color="var(--ctp-red)"
						/>
					</div>
					<p>
						{favoriteRun.totalFavorites}
					</p>
				</div>
			</div>
		</a>
	{/each}
	<div class="see-more paragraph-long-02">
		<ClickableTileImage
			imageSource={Favorite}
			title="View Favorite Runs ({favoriteRuns.length})"
			description="See a list of favorite runs for this user."
			href="/"
		/>
	</div>
</div>

<style lang="scss">
	@use '@carbon/motion' as motion;

	a {
		all: unset;
	}

	.container {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(256px, 1fr));
		gap: 1rem;
		background-color: var(--ctp-mantle);
		padding: 1rem;
		border-radius: 8px;
	}

	.icon {
		max-width: 64px;
		margin: auto;
		padding: 0;
	}

	.run-container {
		display: grid;
		grid-template-columns: auto 1fr;
		gap: 0.5rem;
		background-color: var(--ctp-surface0);
		padding: 1rem;
		border-radius: 0.5rem;
		box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
		transition:
			filter motion.$duration-fast-02 motion.motion(standard, expressive),
			transform motion.$duration-fast-02 motion.motion(standard, expressive);
	}

	.run-container:hover {
		transform: scale(105%);
		filter: brightness(105%) drop-shadow(0px 0px 4px var(--ctp-blue));
	}

	.title {
		font-size: 1.25em;
	}

	.text {
		margin: auto;
	}

	.total-favorites-count {
		display: flex;
		gap: 0.5rem;
		align-items: center;
	}
</style>
