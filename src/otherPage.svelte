<script>
  import { actions, Drawer, Page, Button } from 'ui-components'
  import { onMount } from "svelte"

  export let toggle = true

  $: menuItems = [      
    {},
    {
      url: './',
      label: 'see our components in storybook'
    },
    {
      label: '--break--',
    },
    {
      url: './',
      label: 'see our components in storybook'
    },
    {
      url: './',
      label: 'see our components in storybook'
    },
    {
      label: '--break--',
    },
    {
      url: './',
      label: 'see our components in storybook'
    }
  ]

  onMount(() => {
    //actions are for TopAppBar which Drawer uses as a child.
    $actions = [
      {
        icon: 'info_outline',
        label: 'action demo',
        onClick: () => alert('you clicked an action'),
      }
    ]
  })
</script>

<body>
  <Drawer {menuItems} bind:toggle={toggle} dismissible title="app">
    <span class="pointer" slot="header">
      <img class="w-100" src="/logo.png" alt="logo">
      <Button on:click={() => toggle = !toggle}>Toggle drawer</Button>
    </span>

    <Page title="title">
      <slot/>
    </Page>
  </Drawer>
</body>