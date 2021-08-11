<script>
  import { actions, Drawer, Page, Button } from '@silintl/ui-components'
  import { onMount } from "svelte"

  export let toggle = true

  $: menuItems = [      
    {},
    {
      url: './',
      icon: 'add',
      label: 'see our components in storybook'
    },
    {
      label: '--break--',
    },
    {
      url: './',
      icon: 'add',
      label: 'see'
    },
    {
      url: './',
      icon: 'add',
      button: true,
      label: 'item'
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
  <!-- Drawer must be either modal or dismissible -->
  <Drawer modal hideForTablet miniMenu hasTopAppBar class='auto-width border-white' {menuItems} bind:toggle title="app">
    <span class="pointer" slot="header">
      <img class="w-100" src="/logo.png" alt="logo">
      <Button on:click={() => toggle = !toggle}>Toggle drawer</Button>
    </span>

    <Button slot="actions">end</Button>
    <Button slot="TopAppBar">start</Button>

    <Page title="title">
      <slot/>
    </Page>
  </Drawer>
</body>