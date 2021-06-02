<script>
	import './mdc/_index.scss'
	import { actions, Badge, Button, Card, Checkbox, Snackbar, setNotice, StaticChip, CustomCard, Form, Page, TextField, TopAppBar, Progress } from '@silintl/ui-components'
	import { onMount } from 'svelte'

	let text
	let topics = ['topic1', 'topic2']
	let checked = true
	let appName = 'Demo App'

	onMount(() => {
		//actions are for TopAppBar which Drawer uses.
		$actions = [
			{
				icon: 'info_outline',
				label: 'action demo',
				onClick: () => setNotice('you clicked an action'),
			},
		]
	})

	const clickHandler = () => {
		topics = [...topics, text]
		setNotice('You added a topic!')
	}

	const openMenu = () => setNotice("there isn't a menu yet")
</script>

<TopAppBar on:nav={openMenu}>{appName}</TopAppBar>

<Page title="test page" layout="grid" >
	<div class="mdc-layout-grid__cell mdc-layout-grid__cell--span-12">
		<Page.Subheader>This is a template for ui-components</Page.Subheader>
		
		<Progress.Linear indeterminate/>
	
		<p class='fs-12 gray'>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
	</div>

	<div class="mdc-layout-grid__cell mdc-layout-grid__cell--span-6">
		
		<Card>
			<p class="text-align-center">This is a card</p>

			<Badge color="green">M</Badge>

			<div class="flex justify-center flex-wrap">
				{#each topics as topic}
					<StaticChip>{topic}</StaticChip>
				{/each}
			</div>

			<Form>
				Form
				<TextField label={'Textfield'} bind:value={text} />
			</Form>
			
			<span slot="actions">
				<Button raised on:click={clickHandler}>imported button</Button>
				<Checkbox label='check this out' bind:checked={checked} uppercase/>
			</span>
		</Card>

	</div>
		
	<div class="mdc-layout-grid__cell mdc-layout-grid__cell--span-6">
		<CustomCard buttons={[{label: 'go to ui-components', url: "https://github.com/silinternational/ui-components#readme"}]} icon="face" title='Title goes here' alt='graphic' src="">
			Add some text content here.
		</CustomCard>
	</div>
		
	</Page>

	<Snackbar/>