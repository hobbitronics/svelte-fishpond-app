<script>
	import { Button, Card, Badge, StaticChip } from 'ui-components'
</script>

<main>
	<h1>Hello !</h1>
	<p class='uppercase fs-12 gray'>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>

	<Button raised>imported button</Button>

	<Card>This is a card</Card>

	<br/>

	<Badge color="blue">M</Badge>

	<StaticChip>topic</StaticChip>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>