<script>
	let currentPage = 'home';

	function navigateTo(page) {
		currentPage = page;
	}

	function handleProfileClick(event) {
		if (event.type === 'click' || (event.type === 'keydown' && event.key === 'Enter')) {
			navigateTo('profile');
		}
	}
</script>

<main>
	<div class="layout">
		<nav>
			<div class="profile-avatar" 
				on:click={handleProfileClick} 
				on:keydown={handleProfileClick}
				tabindex="0"
				role="button"
				aria-label="View Profile"
			>
				<svg viewBox="0 0 24 24" width="48" height="48">
					<path fill="currentColor" d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 3c1.66 0 3 1.34 3 3s-1.34 3-3 3-3-1.34-3-3 1.34-3 3-3zm0 14.2c-2.5 0-4.71-1.28-6-3.22.03-1.99 4-3.08 6-3.08 1.99 0 5.97 1.09 6 3.08-1.29 1.94-3.5 3.22-6 3.22z"/>
				</svg>
			</div>
			<button class:active={currentPage === 'home'} on:click={() => navigateTo('home')}>Home</button>
			<button class:active={currentPage === 'profile'} on:click={() => navigateTo('profile')}>Profile</button>
			<button class:active={currentPage === 'channels'} on:click={() => navigateTo('channels')}>Channels</button>
			<button class:active={currentPage === 'schedules'} on:click={() => navigateTo('schedules')}>Schedules</button>
			<button class:active={currentPage === 'inventory'} on:click={() => navigateTo('inventory')}>Inventory</button>
			<button class:active={currentPage === 'dashboard'} on:click={() => navigateTo('dashboard')}>Dashboard</button>
			<button class:active={currentPage === 'personnel'} on:click={() => navigateTo('personnel')}>Personnel</button>
			<button class:active={currentPage === 'orders'} on:click={() => navigateTo('orders')}>Orders</button>
			<button class:active={currentPage === 'products'} on:click={() => navigateTo('products')}>Products</button>
			<button class:active={currentPage === 'stations'} on:click={() => navigateTo('stations')}>Stations</button>
			<button class:active={currentPage === 'clients'} on:click={() => navigateTo('clients')}>Clients</button>
			<button class:active={currentPage === 'maintenance'} on:click={() => navigateTo('maintenance')}>Maintenance</button>
		</nav>

		<div class="content">
			<section>
				{#if currentPage === 'home'}
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
				{:else if currentPage === 'dashboard'}
					<h2>Dashboard</h2>
					<p>Here you can view the dashboard.</p>
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

	.profile-avatar {
		cursor: pointer;
		width: 60px;
		height: 60px;
		background-color: #1C4C96;
		border-radius: 50%;
		display: flex;
		justify-content: center;
		align-items: center;
		margin: 3em 0 3em 0;
		transition: background-color 0.3s ease;
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
		color: #333;
		border: none;
		border-radius: 4px;
		cursor: pointer;
		font-family: 'Roboto', sans-serif;
		font-weight: 400;
		font-size: 0.9em;
		text-align: left;
		transition: all 0.3s ease;
	}

	button:hover {
		background-color: #e0e0e0;
	}

	button.active {
		background-color: #FF0000;
		color: white;
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