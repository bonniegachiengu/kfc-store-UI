<script>
	let currentPage = 'dashboard';
	let userName = "Maya Angela";

	function navigateTo(page) {
		currentPage = page;
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
					<p>Here you can view someone's profile.</p>
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
		margin-top: 3em;
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
		padding: 1em;
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
</style>