<script lang="ts">
	import AvatarCreator from '$lib/components/AvatarCreator.svelte';
</script>

<div class="container">
	<header>
		<h1>Limbus Company - Avatar Creator</h1>
		<p class="subtitle">Create your own Armina avatar</p>
	</header>
	
	<AvatarCreator />
</div>

<style>
	header {
		text-align: center;
		margin-bottom: 3rem;
		padding: 2rem 0;
	}

	h1 {
		font-size: clamp(2rem, 5vw, 3.5rem);
		margin-bottom: 1rem;
		letter-spacing: 2px;
	}

	.subtitle {
		font-size: 1.2rem;
		color: var(--limbus-gold);
		opacity: 0.8;
	}
</style>
