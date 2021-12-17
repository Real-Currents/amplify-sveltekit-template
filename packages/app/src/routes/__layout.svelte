<script context="module">
	import 'sveltekit-ui/style.css';
	import { Layout } from 'sveltekit-ui';
	import Logo from '$lib/assets/static/Logo/index.svelte';
	import { goto } from '$app/navigation';
	import { page } from '$app/stores';
	import AuthTrigger from '$lib/components/Auth/AuthTrigger/index.svelte';
	import AuthModal from '$lib/components/Auth/AuthModal/index.svelte';
	import { Amplify } from 'aws-amplify';
	import awsExports from 'aws-exports';
	Amplify.configure({ ...awsExports, ssr: true });
	import { initAuth } from '$lib/components/Auth/store';
	initAuth();

	const fullNavLinks = [
		{ name: 'Home', path: '/' },
		{ name: 'Settings', path: '/settings' }
	];

	const appFullNavLinks = [
		{ name: 'Home', path: '/' },
		{ name: 'Settings', path: '/settings' }
	];

	const navBarLinks = [
		{ name: 'Home', path: '/' },
		{ name: 'Settings', path: '/settings' }
		// { name: 'Settings', path: '/settings', subLinks: [
		//   { name: 'Profile', path: '/profile' },
		// ]},
	];

	const appNavBarLinks = [
		{ name: 'Home', path: '/' },
		{ name: 'Settings', path: '/settings' }
	];
</script>

<Layout {fullNavLinks} {appFullNavLinks} {navBarLinks} {appNavBarLinks} page={$page} {goto}>
	<div slot="navBarLogo">
		<Logo />
	</div>
	<div slot="appNavBarLogo">
		<Logo />
	</div>
	<div slot="extraLinks">
		<AuthTrigger />
	</div>
	<div slot="content">
		<slot />
	</div>
	<div slot="additional">
		<AuthModal />
	</div>
</Layout>

<style>
	/* :root {
  
  } */
	:global(body) {
		background: var(--bg-med);
		color: var(--contrast-med);
	}
	:global(body.dark) {
		--primary: #a01c8e;
		--primary-dark: #70004e;
		--primary-light: #d01ebe;
		--primary-transparent: #a01c8e5a;
		--red-error: #d6263d;
		--shadow: #0000003a;
		--shadow-soft: #00000040;
		--shadow-strong: #0000008a;
		--tint: #ffffff3a;
		--tint-strong: #ffffff6a;
		--tint-soft: #ffffff1a;
		--white-light: #efefef;
		--white-med: #e6e6e6;
		--white-dark: #c2c2c2;
		--gray-light: #666666;
		--gray-med: #555555;
		--bg-light: #404040;
		--bg-med: #181a20;
		--bg-med-transparent: #181a20dd;
		--bg-highlight: #242424;
		--bg-highlight-strong: #333333;
		--bg-highlight-stronger: #555555;
		--bg-dark: #000000;
		--contrast-soft: #a4aebc;
		--contrast-med: #eaecef;
		--contrast-strong: #fafcff;
		--contrast-overlay: #ffffff20;
		--bg-modal: #2a2a2a;
	}
</style>
