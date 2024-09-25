<script>
	import { onMount, onDestroy } from 'svelte';
	import { fade, fly, slide } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';

	let socket;
	let messages = [];

	let currentPage = 'dashboard';
	let userName = "Maya Angela";
	let currentTab = 'credentials';
	let activeSection = 'education';

	let showContent = false;

	onMount(() => {
		setTimeout(() => {
			showContent = true;
		}, 100);

		socket = new WebSocket('ws://localhost:8000/ws/kfc/');

		socket.onmessage = (event) => {
			const data = JSON.parse(event.data);
			messages = [...messages, data.message];
		};

		socket.onclose = () => {
			console.log('WebSocket connection closed');
		};
	});

	onDestroy(() => {
		if (socket) {
			socket.close();
		}
	});
	
	function sendMessage(message) {
		if (socket && socket.readyState === WebSocket.OPEN) {
			socket.send(JSON.stringify({ message: 'Hello from Svelte' }));
		}
	}

	function navigateTo(page) {
		currentPage = page;
		currentTab = getDefaultTab(page);
	}

	function handleProfileClick(event) {
		if (event.type === 'click' || (event.type === 'keydown' && event.key === 'Enter')) {
			navigateTo('profile');
		}
	}

	function handleLogout() {
		console.log('Logging out...');
	}

	function switchTab(tab) {
		currentTab = tab;
	}

	function toggleSection(section) {
		activeSection = section;
	}

	function getDefaultTab(page) {
		switch(page) {
			case 'profile':
				return 'credentials';
			case 'inventory':
				return 'overview';
			case 'maintenance':
				return 'schedule';
			default:
				return '';
		}
	}

	const sections = [
		{ id: 'education', title: 'Education', content: 'Education content goes here' },
		{ id: 'workHistory', title: 'Work History', content: 'Work History content goes here' },
		{ id: 'training', title: 'Training', content: 'Training content goes here' },
		{ id: 'certifications', title: 'Certifications', content: 'Certifications content goes here' },
		{ id: 'otherSkillsets', title: 'Other Skillsets', content: 'Other Skillsets content goes here' },
		{ id: 'extraCurriculars', title: 'Extra-Curriculars', content: 'Extra-Curriculars content goes here' },
		{ id: 'testimonials', title: 'Testimonials', content: 'Testimonials content goes here' },
	];
</script>

<main>
	<div class="layout">
		<nav>
			<div class="profile-section">
				<div class="profile-avatar" 
					on:click={handleProfileClick} 
					on:keydown={handleProfileClick}
					tabindex="0"
					role="button"
					aria-label="View Profile"
				>
					<img src="/images/avatar.jpg" alt="User Avatar" class="avatar-image" />
				</div>
				<span class="profile-name">{userName}</span>
			</div>
			{#each ['dashboard', 'channels', 'schedules', 'inventory', 'personnel', 'orders', 'products', 'stations', 'clients', 'maintenance'] as page, i}
				<button 
					class:active={currentPage === page} 
					on:click={() => navigateTo(page)}
					in:fly={{ y: 20, delay: i * 50, duration: 300, easing: quintOut }}
				>
					<img src="/images/{page}.png" alt="{page} Icon" class="nav-icon" />
					{page.charAt(0).toUpperCase() + page.slice(1)}
				</button>
			{/each}
			<div class="nav-spacer"></div>
			<button class="logout-button" on:click={handleLogout} in:fly={{ y: 20, delay: 500, duration: 300, easing: quintOut }}>
				<img src="/images/log-out.png" alt="Log Out Icon" class="nav-icon" />
				Log Out
			</button>
		</nav>

		<div class="content">
			{#if showContent}
			<section in:fade={{duration: 300}}>
				{#if currentPage === 'dashboard'}
					<h2>Welcome to KFC Management</h2>
					<p>Select a section from the navigation menu to get started.</p>
				{:else if currentPage === 'profile'}
					<h2>Profile</h2>
					<div class="tabs">
						{#each ['credentials', 'resume', 'documents', 'preferences', 'messages'] as tab, i}
							<button 
								class:active={currentTab === tab} 
								on:click={() => switchTab(tab)}
								in:fly={{ x: -20, delay: i * 50, duration: 300, easing: quintOut }}
							>
								{tab.charAt(0).toUpperCase() + tab.slice(1)}
							</button>
						{/each}
					</div>
					<div class="tab-content" in:fade={{duration: 300}}>
						{#if currentTab === 'credentials'}
							<div class="credentials-content">
								<div class="avatar-container">
									<img src="/images/avatar.jpg" alt="User Avatar" class="tall-avatar">
								</div>
								<div class="tab-content-data user-info">
									<div class="user-info-header">
										<p class="user-info-name"><strong>{userName}</strong></p>
										<button class="crud-button"><img class="crud-icon" src="/images/edit.png" alt="edit"/></button>
									</div>
									<p class="user-info-position"><strong>Restaurant Manager/KFC</strong></p>
									<ul class="user-info-group">
										<li><img class="user-info-icon" src="/images/id.png" alt="id"/><p class="user-info-item"><strong></strong> KFC12345</p></li>
										<li>
											<img class="user-info-icon" src="/images/nationality.png" alt="id"/>
											<p class="user-info-item">
												<strong></strong>
												<img src="https://flagcdn.com/w20/ke.png" alt="Kenyan flag" style="vertical-align: middle;"/>
											</p>
										</li>
										<li><img class="user-info-icon" src="/images/address.png" alt="id"/><p class="user-info-item"><strong></strong> 123 Main St, Anytown, USA</p></li>
										<li><img class="user-info-icon" src="/images/email.png" alt="id"/><p class="user-info-item"><strong></strong> {userName.toLowerCase().replace(' ', '.')}@kfc.com</p></li>
										<li><img class="user-info-icon" src="/images/phone.png" alt="id"/><p class="user-info-item"><strong></strong> +1 (555) 123-4567</p></li>
									</ul>
									<br>
									<ul class="social-media-links">
										<li><img src="/images/x-icon.png" alt="x" class="social-icon" /> {userName.toLowerCase().replace(' ', '_')}</li>
										<li><img src="/images/tik-icon.png" alt="tiktok" class="social-icon" /> {userName.toLowerCase().replace(' ', '_')}</li>
										<li><img src="/images/insta-icon.png" alt="Instagram" class="social-icon" /> {userName.toLowerCase().replace(' ', '_')}_kfc</li>
									</ul>
								</div>
							</div>
						{:else if currentTab === 'resume'}
						<div class="resume-content">
							<div class="left-column">
								<div class="avatar-container">
									<img src="/images/avatar.jpg" alt="User Avatar" class="tall-avatar">
								</div>
								<div class="tab-content-data user-info">
									<div class="user-info-header">
										<p class="user-info-name"><strong>{userName}</strong></p>
										<button class="crud-button"><img class="crud-icon" src="/images/edit.png" alt="edit"/></button>
									</div>
									<p class="user-info-position"><strong>Restaurant Manager/KFC</strong></p>
									<ul class="user-info-group">
										<li><img class="user-info-icon" src="/images/id.png" alt="id"/><p class="user-info-item"><strong></strong> KFC12345</p></li>
										<li>
											<img class="user-info-icon" src="/images/nationality.png" alt="id"/>
											<p class="user-info-item">
												<strong></strong>
												<img src="https://flagcdn.com/w20/ke.png" alt="Kenyan flag" style="vertical-align: middle;"/>
											</p>
										</li>
										<li><img class="user-info-icon" src="/images/address.png" alt="id"/><p class="user-info-item"><strong></strong> 123 Main St, Anytown, USA</p></li>
										<li><img class="user-info-icon" src="/images/email.png" alt="id"/><p class="user-info-item"><strong></strong> {userName.toLowerCase().replace(' ', '.')}@kfc.com</p></li>
										<li><img class="user-info-icon" src="/images/phone.png" alt="id"/><p class="user-info-item"><strong></strong> +1 (555) 123-4567</p></li>
									</ul>
								</div>
							</div>
							<div class="resume-sections">
								{#each sections as section, i}
									<div class="accordion-item" in:fly={{ y: 20, delay: i * 50, duration: 300, easing: quintOut }}>
										<button class="accordion-toggle" on:click={() => toggleSection(section.id)}>
											{section.title}
											<span class="toggle-icon">{activeSection === section.id ? '▼' : '▶'}</span>
										</button>
										{#if activeSection === section.id}
											<div class="accordion-content" in:slide={{duration: 300}}>
												<p>{section.content}</p>
											</div>
										{/if}
									</div>
								{/each}
							</div>
						</div>
						{:else if currentTab === 'documents'}
							<h3>Documents</h3>
							<!-- Add documents content here -->
						{:else if currentTab === 'preferences'}
							<h3>Preferences</h3>
							<!-- Add preferences content here -->
						{:else if currentTab === 'messages'}
							<h3>Messages</h3>
							<!-- Add messages content here -->
						{/if}
					</div>
				{:else if currentPage === 'channels'}
					<h2>Channels</h2>
					<p>Here you can manage point of sale channels.</p>
				{:else if currentPage === 'schedules'}
					<h2>Schedules</h2>
					<p>Here you can manage schedules.</p>
				{:else if currentPage === 'inventory'}
					<h2>Inventory</h2>
					<p>Here you can manage inventory.</p>
				{:else if currentPage === 'personnel'}
					<h2>Personnel</h2>
					<p>Here you can manage personnel.</p>
				{:else if currentPage === 'orders'}
					<h2>Orders</h2>
					<p>Here you can manage orders.</p>
				{:else if currentPage === 'products'}
					<h2>Products</h2>
					<p>Here you can manage products.</p>
				{:else if currentPage === 'stations'}
					<h2>Stations</h2>
					<p>Here you can manage stations.</p>
				{:else if currentPage === 'clients'}
					<h2>Clients</h2>
					<p>Here you can manage clients.</p>
				{:else if currentPage === 'maintenance'}
					<h2>Maintenance</h2>
					<p>Here you can manage maintenance.</p>
				{/if}
			</section>
			{/if}
		</div>
	</div>
</main>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500&display=swap');

	main {
		font-family: 'PT Sans', sans-serif;
		height: 100vh;
		background-color: #f5f5f5;
	}

	.layout {
		display: flex;
		height: 100%;
	}

	nav {
		width: 200px;
		padding: 1em;
		display: flex;
		flex-direction: column;
		align-items: center;
		border-right: 1px solid #e0e0e0;
	}

	.profile-section {
		display: flex;
		flex-direction: column;
		align-items: center;
		margin-bottom: 2em;
	}

	.profile-avatar {
		cursor: pointer;
		width: 100px;
		height: 100px;
		background-color: #1C4C96;
		border-radius: 50%;
		display: flex;
		justify-content: center;
		align-items: center;
		margin-top: 2em;
		margin-bottom: 0.5em;
		transition: background-color 0.3s ease;
	}

	.avatar-image {
		width: 100%;
		height: 100%;
		border-radius: 50%;
		object-fit: cover;
	}

	.profile-name {
		width: 100%;
		font-size: 1.1em;
		font-weight: 800;
		color: #333;
		margin-bottom: 0.3em;
	}

	.profile-avatar:hover, .profile-avatar:focus {
		background-color: #2A69D4;
		outline: none;
	}

	button {
		width: 100%;
		margin: 0.3em 0;
		padding: 0.4em 0.8em;
		background-color: transparent;
		color: #6a6969;
		border: none;
		border-radius: 4px;
		cursor: pointer;
		font-family: 'PT Sans', sans-serif;
		font-weight: 600;
		font-size: 0.8em;
		text-align: left;
		transition: all 0.3s ease;
		display: flex;
		align-items: center;
	}

	button:hover {
		background-color: #e0e0e0;
	}

	button.active {
		background-color: #ff593b;
		color: white;
	}

	.nav-icon {
		width: 20px;
		height: 20px;
		margin-right: 0.5em;
	}

	.content {
		flex-grow: 1;
		overflow-y: auto;
		text-align: left;
	}

	section {
		padding: 2em;
		border-radius: 8px;
	}

	.nav-spacer {
		flex-grow: 1;
	}

	.logout-button {
		margin-top: auto;
		color: #6a6969;
	}

	.tabs {
		display: flex;
		margin-bottom: 1em;
	}

	.tabs button {
		padding: 0.5em 1em;
		margin-right: 0.5em;
		background-color: #f0f0f0;
		border: none;
		border-radius: 4px;
		cursor: pointer;
		transition: background-color 0.3s ease;
	}

	.tabs button:hover {
		background-color: #e0e0e0;
	}

	.tabs button.active {
		background-color: #ff593b;
		color: white;
	}

	.tab-content {
		background-color: #e0e0e0;
		border-radius: 4px;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
	}

	.tab-content-data {
		padding: 1em;
	}

	.credentials-content {
		display: flex;
		gap: 2em;
	}

	.avatar-container {
		flex-shrink: 0;
	}

	.tall-avatar {
		width: 300px;
		height: 500px;
		object-fit: cover;
	}

	.user-info {
		flex-grow: 1;
	}

	.user-info p {
		margin: 0.5em 0;
	}

	.user-info ul {
		list-style-type: none;
		padding-left: 1em;
	}

	.social-media-links {
		display: flex;
		flex-direction: column;
		gap: 0.5em;
	}

	.social-media-links li {
		display: flex;
		align-items: center;
		font-size: 1em;
		font-weight: 400;
		color: #2c2b2b;
	}

	.social-media-links img {
		width: 20px;
		height: 20px;
		margin-right: 0.5em;
	}

	@media (max-width: 768px) {
		.layout {
			flex-direction: column;
		}

		nav {
			width: 100%;
			border-right: none;
			border-bottom: 1px solid #e0e0e0;
		}

		.content {
			padding: 1em;
		}
	}

	.user-info-name {
		font-size: 2.5em;
		font-weight: 500;
		font-family: 'PT Sans', sans-serif;
		margin-right: auto; /* This will push the name to the left */
	}

	.user-info-item {
		font-size: 1em;
		font-weight: 600;
		color: #6f6b6a;
	}

	.user-info-position {
		font-size: 1.3em;
		font-weight: 500;
		color: #2b78ff;
		margin-top: 0.5em;
	}

	.user-info-icon {
		width: 20px;
		height: 20px;
		margin-right: 0.5em;
	}

	.user-info-group {
		display: flex;
		flex-direction: column;
		padding-top: 1em;
	}

	.user-info-group li {
		display: flex;
		align-items: center;
	}

	.user-info-header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		width: 100%;
	}

	.crud-button {
		padding: 5px 10px;
		border: none;
		border-radius: 4px;
		cursor: pointer;
		font-size: 0.9em;
		display: flex;
		align-items: center;
		width: auto; /* This allows the button to size based on content */
		min-width: 40px; /* Minimum width to ensure the icon fits */
		justify-content: center;
	}

	.crud-icon {
		width: 20px;
		height: 20px;
	}

	.resume-content {
		display: flex;
		gap: 2em;
	}

	.left-column {
		flex-shrink: 0;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.resume-sections {
		flex-grow: 1;
		display: flex;
		flex-direction: column;
	}

	.accordion-item {
		border-radius: 4px;
		margin-bottom: 10px;
	}

	.accordion-toggle {
		width: 100%;
		text-align: left;
		padding: 10px;
		border: none;
		border-radius: 5px;
		cursor: pointer;
		transition:  0.3s ease;
		display: flex;
		justify-content: space-between;
		align-items: center;
		color: #474544;
		font-size: 1.1em;
		font-weight: 600;
	}

	.accordion-toggle:hover {
		background-color: #e0e0e0;
	}

	.toggle-icon {
		font-size: 1.2em;
		font-weight: bold;
		float: right;
	}

	.accordion-content {
		padding: 10px;
		font-size: 1em;
		font-weight: 450;
		color: #696766;
		border-radius: 0 0 5px 5px;
	}

</style>