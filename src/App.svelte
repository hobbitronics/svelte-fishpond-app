<script>
	import { Button, Card, Badge, StaticChip, CustomCard, Form, Page, TextField } from 'ui-components'

	let text

	let topics = ['topic1', 'topic2']
</script>


<Page title="test" layout="grid" >
	<div class="mdc-layout-grid__cell mdc-layout-grid__cell--span-12">
		<Page.Subheader>This is a template for ui-components</Page.Subheader>
	
		<p class='fs-12 gray'>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
	</div>

	<div class="mdc-layout-grid__cell mdc-layout-grid__cell--span-6">
		
		<Card>
			<p class="align-center">This is a card</p>

			<Badge color="green">M</Badge>

			<div class="flex justify-center flex-wrap">
				{#each topics as topic}
					<StaticChip>{topic}</StaticChip>
				{/each}
			</div>

			<Form>
				Form
				<TextField placeholder='Textfield' bind:value={text} />
			</Form>
			
			<span slot="actions">
				<Button raised on:click={() => topics = [...topics, text]}>imported button</Button>
			</span>
		</Card>

	</div>
		
	<div class="mdc-layout-grid__cell mdc-layout-grid__cell--span-6">
		<CustomCard buttons={[{label: 'go to ui-components', url: "https://github.com/silinternational/ui-components#readme"}]} icon="face" title='Title goes here' alt='graphic' src="">
			Add some text content here.
		</CustomCard>
	</div>
		
	</Page>