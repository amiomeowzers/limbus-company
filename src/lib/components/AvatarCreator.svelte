<script lang="ts">
	type AvatarPart = {
		id: string;
		name: string;
		options: { id: string; name: string; color?: string }[];
	};

	type Environment = {
		id: string;
		name: string;
		gradient: string;
		description: string;
	};

	// Avatar customization options
	const avatarParts: AvatarPart[] = [
		{
			id: 'skin',
			name: 'Skin Tone',
			options: [
				{ id: 'fair', name: 'Fair', color: '#FFE0BD' },
				{ id: 'medium', name: 'Medium', color: '#D4A373' },
				{ id: 'tan', name: 'Tan', color: '#C68642' },
				{ id: 'dark', name: 'Dark', color: '#8D5524' }
			]
		},
		{
			id: 'hair',
			name: 'Hair Style',
			options: [
				{ id: 'short', name: 'Short' },
				{ id: 'medium', name: 'Medium' },
				{ id: 'long', name: 'Long' },
				{ id: 'armina', name: 'Armina Style' }
			]
		},
		{
			id: 'hairColor',
			name: 'Hair Color',
			options: [
				{ id: 'black', name: 'Black', color: '#2C2C2C' },
				{ id: 'brown', name: 'Brown', color: '#6F4E37' },
				{ id: 'blonde', name: 'Blonde', color: '#F5DEB3' },
				{ id: 'red', name: 'Red', color: '#8B0000' },
				{ id: 'white', name: 'White', color: '#E8E8E8' },
				{ id: 'blue', name: 'Blue', color: '#4169E1' }
			]
		},
		{
			id: 'eyes',
			name: 'Eye Color',
			options: [
				{ id: 'brown', name: 'Brown', color: '#6F4E37' },
				{ id: 'blue', name: 'Blue', color: '#4169E1' },
				{ id: 'green', name: 'Green', color: '#228B22' },
				{ id: 'red', name: 'Red', color: '#8B0000' },
				{ id: 'gold', name: 'Gold', color: '#D4AF37' }
			]
		},
		{
			id: 'outfit',
			name: 'Outfit',
			options: [
				{ id: 'sinner', name: 'Sinner Uniform' },
				{ id: 'casual', name: 'Casual' },
				{ id: 'formal', name: 'Formal' },
				{ id: 'armina', name: 'Armina Outfit' }
			]
		},
		{
			id: 'accessory',
			name: 'Accessories',
			options: [
				{ id: 'none', name: 'None' },
				{ id: 'glasses', name: 'Glasses' },
				{ id: 'earrings', name: 'Earrings' },
				{ id: 'necklace', name: 'Necklace' },
				{ id: 'hat', name: 'Hat' }
			]
		}
	];

	// Environment/Background options
	const environments: Environment[] = [
		{
			id: 'limbus-bus',
			name: 'Limbus Company Bus',
			gradient: 'linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%)',
			description: 'Inside the iconic Limbus Company bus'
		},
		{
			id: 'city',
			name: 'The City',
			gradient: 'linear-gradient(135deg, #2c3e50 0%, #34495e 50%, #7f8c8d 100%)',
			description: 'Dark streets of The City'
		},
		{
			id: 'office',
			name: 'Limbus Office',
			gradient: 'linear-gradient(135deg, #8B0000 0%, #5c0000 50%, #2d0000 100%)',
			description: 'Company office interior'
		},
		{
			id: 'mirror',
			name: 'Mirror Dungeon',
			gradient: 'linear-gradient(135deg, #1e3a8a 0%, #312e81 50%, #4c1d95 100%)',
			description: 'Mysterious mirror dimension'
		},
		{
			id: 'night',
			name: 'Night Sky',
			gradient: 'linear-gradient(135deg, #0f0f23 0%, #1a1a40 50%, #2d2d5f 100%)',
			description: 'Under the stars'
		},
		{
			id: 'golden',
			name: 'Golden Bough',
			gradient: 'linear-gradient(135deg, #D4AF37 0%, #AA8B2E 50%, #806F25 100%)',
			description: 'Radiant golden energy'
		}
	];

	// State
	let selectedOptions = $state<Record<string, string>>({
		skin: 'fair',
		hair: 'armina',
		hairColor: 'black',
		eyes: 'brown',
		outfit: 'armina',
		accessory: 'none'
	});

	let selectedEnvironment = $state<string>('limbus-bus');

	function getSelectedOption(partId: string): string {
		return selectedOptions[partId] || '';
	}

	function updateSelection(partId: string, optionId: string) {
		selectedOptions[partId] = optionId;
	}

	function getCurrentEnvironment(): Environment {
		return environments.find(env => env.id === selectedEnvironment) || environments[0];
	}

	function exportAvatar() {
		const avatarData = {
			...selectedOptions,
			environment: selectedEnvironment,
			timestamp: new Date().toISOString()
		};
		
		const dataStr = JSON.stringify(avatarData, null, 2);
		const dataUri = 'data:application/json;charset=utf-8,' + encodeURIComponent(dataStr);
		
		const exportFileDefaultName = `armina-avatar-${Date.now()}.json`;
		
		const linkElement = document.createElement('a');
		linkElement.setAttribute('href', dataUri);
		linkElement.setAttribute('download', exportFileDefaultName);
		linkElement.click();
	}

	function randomize() {
		avatarParts.forEach(part => {
			const randomOption = part.options[Math.floor(Math.random() * part.options.length)];
			selectedOptions[part.id] = randomOption.id;
		});
		
		const randomEnv = environments[Math.floor(Math.random() * environments.length)];
		selectedEnvironment = randomEnv.id;
	}
</script>

<div class="avatar-creator">
	<div class="preview-section">
		<div class="environment-preview" style="background: {getCurrentEnvironment().gradient}">
			<div class="avatar-display">
				<div class="avatar-placeholder">
					<div class="avatar-icon">
						<svg width="200" height="200" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
							<!-- Head -->
							<circle cx="100" cy="70" r="40" fill="{avatarParts[0].options.find(o => o.id === getSelectedOption('skin'))?.color || '#FFE0BD'}" stroke="#2c2c2c" stroke-width="2"/>
							
							<!-- Hair -->
							<ellipse cx="100" cy="50" rx="45" ry="30" fill="{avatarParts[2].options.find(o => o.id === getSelectedOption('hairColor'))?.color || '#2C2C2C'}"/>
							
							<!-- Eyes -->
							<circle cx="90" cy="65" r="5" fill="{avatarParts[3].options.find(o => o.id === getSelectedOption('eyes'))?.color || '#6F4E37'}"/>
							<circle cx="110" cy="65" r="5" fill="{avatarParts[3].options.find(o => o.id === getSelectedOption('eyes'))?.color || '#6F4E37'}"/>
							
							<!-- Body -->
							<rect x="60" y="105" width="80" height="90" rx="10" fill="#4a4a4a" stroke="#2c2c2c" stroke-width="2"/>
							
							<!-- Arms -->
							<rect x="40" y="110" width="20" height="60" rx="10" fill="{avatarParts[0].options.find(o => o.id === getSelectedOption('skin'))?.color || '#FFE0BD'}" stroke="#2c2c2c" stroke-width="2"/>
							<rect x="140" y="110" width="20" height="60" rx="10" fill="{avatarParts[0].options.find(o => o.id === getSelectedOption('skin'))?.color || '#FFE0BD'}" stroke="#2c2c2c" stroke-width="2"/>
						</svg>
					</div>
					<div class="avatar-details">
						<p class="environment-name">{getCurrentEnvironment().name}</p>
						<p class="environment-desc">{getCurrentEnvironment().description}</p>
					</div>
				</div>
			</div>
		</div>
	</div>

	<div class="customization-section">
		<div class="section-header">
			<h2>Customize Avatar</h2>
			<div class="action-buttons">
				<button class="btn-secondary" onclick={randomize}>
					🎲 Randomize
				</button>
				<button class="btn-primary" onclick={exportAvatar}>
					💾 Export
				</button>
			</div>
		</div>

		<div class="customization-groups">
			<!-- Avatar Parts -->
			{#each avatarParts as part}
				<div class="customization-group">
					<h3>{part.name}</h3>
					<div class="options-grid">
						{#each part.options as option}
							<button
								class="option-btn"
								class:selected={getSelectedOption(part.id) === option.id}
								onclick={() => updateSelection(part.id, option.id)}
							>
								{#if option.color}
									<span class="color-preview" style="background: {option.color}"></span>
								{/if}
								<span class="option-name">{option.name}</span>
							</button>
						{/each}
					</div>
				</div>
			{/each}

			<!-- Environment Selection -->
			<div class="customization-group environment-group">
				<h3>🌍 Environment / Background</h3>
				<div class="environment-grid">
					{#each environments as env}
						<button
							class="environment-btn"
							class:selected={selectedEnvironment === env.id}
							onclick={() => selectedEnvironment = env.id}
							style="background: {env.gradient}"
						>
							<span class="env-name">{env.name}</span>
							<span class="env-desc">{env.description}</span>
						</button>
					{/each}
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	.avatar-creator {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 2rem;
		margin-top: 2rem;
	}

	.preview-section {
		position: sticky;
		top: 2rem;
		height: fit-content;
	}

	.environment-preview {
		border-radius: 16px;
		padding: 3rem;
		box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
		border: 2px solid var(--limbus-border);
		min-height: 500px;
		display: flex;
		align-items: center;
		justify-content: center;
		transition: all 0.5s ease;
	}

	.avatar-display {
		text-align: center;
	}

	.avatar-placeholder {
		background: rgba(255, 255, 255, 0.1);
		backdrop-filter: blur(10px);
		border-radius: 12px;
		padding: 2rem;
		border: 1px solid rgba(255, 255, 255, 0.2);
	}

	.avatar-icon {
		margin-bottom: 1rem;
	}

	.avatar-details {
		margin-top: 1.5rem;
	}

	.environment-name {
		font-size: 1.5rem;
		font-weight: bold;
		color: var(--limbus-gold);
		margin-bottom: 0.5rem;
	}

	.environment-desc {
		color: rgba(255, 255, 255, 0.8);
		font-size: 0.9rem;
	}

	.customization-section {
		overflow-y: auto;
		max-height: 90vh;
		padding-right: 1rem;
	}

	.section-header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 2rem;
		padding-bottom: 1rem;
		border-bottom: 2px solid var(--limbus-border);
	}

	.action-buttons {
		display: flex;
		gap: 1rem;
	}

	.btn-primary, .btn-secondary {
		padding: 0.75rem 1.5rem;
		border: none;
		border-radius: 8px;
		font-size: 1rem;
		font-weight: 600;
		transition: all 0.3s ease;
	}

	.btn-primary {
		background: var(--limbus-gold);
		color: var(--limbus-darker);
	}

	.btn-primary:hover {
		background: #FFD700;
		transform: translateY(-2px);
	}

	.btn-secondary {
		background: var(--limbus-red);
		color: white;
	}

	.btn-secondary:hover {
		background: #A52A2A;
	}

	.customization-groups {
		display: flex;
		flex-direction: column;
		gap: 2rem;
	}

	.customization-group {
		background: rgba(255, 255, 255, 0.05);
		border: 1px solid var(--limbus-border);
		border-radius: 12px;
		padding: 1.5rem;
	}

	.customization-group h3 {
		margin-bottom: 1rem;
		font-size: 1.2rem;
	}

	.options-grid {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
		gap: 0.75rem;
	}

	.option-btn {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		padding: 0.75rem 1rem;
		background: rgba(255, 255, 255, 0.05);
		border: 2px solid var(--limbus-border);
		border-radius: 8px;
		color: var(--limbus-text);
		font-size: 0.9rem;
		transition: all 0.3s ease;
	}

	.option-btn:hover {
		background: rgba(255, 255, 255, 0.1);
		border-color: var(--limbus-gold);
	}

	.option-btn.selected {
		background: var(--limbus-gold);
		color: var(--limbus-darker);
		border-color: var(--limbus-gold);
		font-weight: 600;
	}

	.color-preview {
		width: 20px;
		height: 20px;
		border-radius: 50%;
		border: 2px solid rgba(255, 255, 255, 0.3);
		flex-shrink: 0;
	}

	.environment-grid {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
		gap: 1rem;
	}

	.environment-btn {
		padding: 2rem 1rem;
		border: 3px solid transparent;
		border-radius: 12px;
		color: white;
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
		text-align: center;
		transition: all 0.3s ease;
		position: relative;
		overflow: hidden;
	}

	.environment-btn::before {
		content: '';
		position: absolute;
		inset: 0;
		background: rgba(0, 0, 0, 0.3);
		transition: opacity 0.3s ease;
	}

	.environment-btn:hover::before {
		opacity: 0;
	}

	.environment-btn.selected {
		border-color: var(--limbus-gold);
		box-shadow: 0 0 20px rgba(212, 175, 55, 0.5);
	}

	.env-name, .env-desc {
		position: relative;
		z-index: 1;
		text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.8);
	}

	.env-name {
		font-weight: 700;
		font-size: 1.1rem;
	}

	.env-desc {
		font-size: 0.85rem;
		opacity: 0.9;
	}

	@media (max-width: 1024px) {
		.avatar-creator {
			grid-template-columns: 1fr;
		}

		.preview-section {
			position: relative;
			top: 0;
		}

		.customization-section {
			max-height: none;
		}
	}

	@media (max-width: 640px) {
		.options-grid {
			grid-template-columns: 1fr 1fr;
		}

		.environment-grid {
			grid-template-columns: 1fr;
		}

		.section-header {
			flex-direction: column;
			gap: 1rem;
			align-items: flex-start;
		}

		.action-buttons {
			width: 100%;
			flex-direction: column;
		}

		.btn-primary, .btn-secondary {
			width: 100%;
		}
	}
</style>
