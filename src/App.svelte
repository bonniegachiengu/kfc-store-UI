<script>
	let currentPage = 'dashboard';
	let userName = "Maya Angela";
	let currentTab = 'credentials';

	function navigateTo(page) {
		currentPage = page;
		// Reset the tab when changing pages
		currentTab = getDefaultTab(page);
	}

	function handleProfileClick(event) {
		if (event.type === 'click' || (event.type === 'keydown' && event.key === 'Enter')) {
			navigateTo('profile');
		}
	}

	function handleLogout() {
		// Add logout functionality here
		console.log('Logging out...');
	}

	function switchTab(tab) {
		currentTab = tab;
	}

	function getDefaultTab(page) {
		switch(page) {
			case 'profile':
				return 'credentials';
			case 'inventory':
				return 'overview';
			case 'maintenance':
				return 'schedule';
			// Add more cases for other pages as needed
			default:
				return '';
		}
	}
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
			<button class:active={currentPage === 'dashboard'} on:click={() => navigateTo('dashboard')}>
				<img src="/images/dashboard.png" alt="Dashboard Icon" class="nav-icon" />
				Dashboard
			</button>
			<button class:active={currentPage === 'channels'} on:click={() => navigateTo('channels')}>
				<img src="/images/channels.png" alt="Channels Icon" class="nav-icon" />
				Channels
			</button>
			<button class:active={currentPage === 'schedules'} on:click={() => navigateTo('schedules')}>
				<img src="/images/schedules.png" alt="Schedules Icon" class="nav-icon" />
				Schedules
			</button>
			<button class:active={currentPage === 'inventory'} on:click={() => navigateTo('inventory')}>
				<img src="/images/inventory.png" alt="Inventory Icon" class="nav-icon" />
				Inventory
			</button>
			<button class:active={currentPage === 'personnel'} on:click={() => navigateTo('personnel')}>
				<img src="/images/personnel.png" alt="Personnel Icon" class="nav-icon" />
				Personnel
			</button>
			<button class:active={currentPage === 'orders'} on:click={() => navigateTo('orders')}>
				<img src="/images/orders.png" alt="Orders Icon" class="nav-icon" />
				Orders
			</button>
			<button class:active={currentPage === 'products'} on:click={() => navigateTo('products')}>
				<img src="/images/products.png" alt="Products Icon" class="nav-icon" />
				Products
			</button>
			<button class:active={currentPage === 'stations'} on:click={() => navigateTo('stations')}>
				<img src="/images/stations.png" alt="Stations Icon" class="nav-icon" />
				Stations
			</button>
			<button class:active={currentPage === 'clients'} on:click={() => navigateTo('clients')}>
				<img src="/images/clients.png" alt="Clients Icon" class="nav-icon" />
				Clients
			</button>
			<button class:active={currentPage === 'maintenance'} on:click={() => navigateTo('maintenance')}>
				<img src="/images/maintenance.png" alt="Maintenance Icon" class="nav-icon" />
				Maintenance
			</button>
			<div class="nav-spacer"></div>
			<button class="logout-button" on:click={handleLogout}>
				<img src="/images/log-out.png" alt="Log Out Icon" class="nav-icon" />
				Log Out
			</button>
		</nav>

		<div class="content">
			<section>
				{#if currentPage === 'dashboard'}
					<h2>Welcome to KFC Management</h2>
					<p>Select a section from the navigation menu to get started.</p>
				{:else if currentPage === 'profile'}
					<h2>Profile</h2>
					<div class="tabs">
						<button class:active={currentTab === 'credentials'} on:click={() => switchTab('credentials')}>Credentials</button>
						<button class:active={currentTab === 'resume'} on:click={() => switchTab('resume')}>Resume</button>
						<button class:active={currentTab === 'documents'} on:click={() => switchTab('documents')}>Documents</button>
						<button class:active={currentTab === 'preferences'} on:click={() => switchTab('preferences')}>Preferences</button>
						<button class:active={currentTab === 'messages'} on:click={() => switchTab('messages')}>Messages</button>
					</div>
					<div class="tab-content">
						{#if currentTab === 'credentials'}
							<div class="credentials-content">
								<div class="avatar-container">
									<img src="/images/avatar.jpg" alt="User Avatar" class="tall-avatar">
								</div>
								<div class="user-info">
									<p class="user-info-name"><strong>{userName}</strong></p>
									<p class="user-info-position"><strong>Restaurant Manager/KFC</strong></p>
									<ul class="user-info-group">
										<li><img class="user-info-icon" src="/images/id.png" alt="id"/><p class="user-info-item"><strong></strong> KFC12345</p></li>
										<li><img class="user-info-icon" src="/images/nationality.png" alt="id"/><p class="user-info-item"><strong></strong> 🇺🇸</p></li>
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
							<h3>Resume</h3>
							<!-- Add resume content here -->
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
					<!-- Add tabs for inventory page if needed -->
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
					<!-- Add tabs for maintenance page if needed -->
					<p>Here you can manage maintenance.</p>
				{/if}
			</section>
		</div>
	</div>
</main>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500&display=swap');

	main {
		font-family: 'Roboto', sans-serif;
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
		margin-top: 1em;
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
		font-family: 'Roboto', sans-serif;
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
		background-color: #FF0000;
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

	.tabs button.active {
		background-color: #FF0000;
		color: white;
	}

	.tab-content {
		background-color: #e0e0e0;
		padding: 1em;
		border-radius: 4px;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
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
		border-radius: 10px;
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
		font-weight: 700;
	}

	.user-info-item {
		font-size: 1em;
		font-weight: 500;
	}

	.user-info-position {
		font-size: 1.3em;
		font-weight: 700;
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
</style>