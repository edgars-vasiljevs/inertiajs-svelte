<script context="module">
  export const h = (component, props, children) => {
    return {
      component,
      ...(props ? { props } : {}),
      ...(children ? { children } : {}),
    }
  }
</script>

<script>
  import store from './store'

  export let component
  export let props = {}
  export let children = []

  let update = (c) => c === $store.component.default && (!children || !children.length) ? $store.key : null
  $: key = update(component) || key
</script>

{#if $store.component}
  {#key key}
    <svelte:component this={component} {...props}>
      {#each children as child, index (component && component.length === index ? $store.key : null)}
        <svelte:self {...child} />
      {/each}
    </svelte:component>
  {/key}
{/if}
