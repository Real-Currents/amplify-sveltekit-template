<script lang="ts">
  import { onDestroy } from 'svelte';
  import { setupMachine, route, toSignIn } from '$lib/components/authStore';
  import AmplifyTabs from './primitives/AmplifyTabs.svelte';
  import AmplifyTabItem from './primitives/AmplifyTabItem.svelte';
  import ConfirmSignUp from './ConfirmSignUp.svelte';

  export let initialState = undefined;
  export let loginMechanisms = undefined;
  export let services = undefined;
  export let signUpAttributes = undefined;
  export let socialProviders = undefined;

  const _subscription = setupMachine(
    initialState,
    loginMechanisms,
    services,
    signUpAttributes,
    socialProviders
  );

  onDestroy(() => {
    if (_subscription) _subscription.unsubscribe();
  });
</script>

{#if $route !== 'authenticated'}
  <div data-amplify-authenticator>
    <div data-amplify-container>
      <!--Slot header goes here-->
      <div data-amplify-router>
        {#if $route === 'signIn' || $route === 'signUp'}
          <AmplifyTabs let:tabs>
            {#each tabs as tab}
              <AmplifyTabItem
                active={tab.active}
                id={tab.id}
                labelledById={tab.labelledById}
                tabIndex={tab.tabIndex}
              >
                <svelte:component this={tab.component} />
              </AmplifyTabItem>
            {/each}
          </AmplifyTabs>
        {/if}
        {#if $route === 'resetPassword'}
          <p>reset password</p>
          <button on:click={toSignIn}>To Sign In</button>
        {/if}
        {#if $route === 'confirmSignUp'}
          <ConfirmSignUp />
        {/if}
      </div>
    </div>
  </div>
{/if}
{#if $route === 'authenticated'}
  <slot />
{/if}
