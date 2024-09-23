<script>
	// State variable to keep track of the current page
	let currentPage = 'home';

	// Function to handle navigation between pages
	function navigateTo(page) {
		currentPage = page;
	}
</script>

<main>
	<h1>KFC Protégé</h1>
	
	<!-- Navigation menu -->
	<nav>
		<button on:click={() => navigateTo('home')}>Home</button>
		<button on:click={() => navigateTo('profile')}>Profile</button>
		<button on:click={() => navigateTo('channels')}>Channels</button>
		<button on:click={() => navigateTo('schedules')}>Schedules</button>
		<button on:click={() => navigateTo('inventory')}>Inventory</button>
		<button on:click={() => navigateTo('dashboard')}>Dashboard</button>
		<button on:click={() => navigateTo('personnel')}>Personnel</button>
		<button on:click={() => navigateTo('orders')}>Orders</button>
		<button on:click={() => navigateTo('products')}>Products</button>
		<button on:click={() => navigateTo('stations')}>Stations</button>
		<button on:click={() => navigateTo('clients')}>Clients</button>
		<button on:click={() => navigateTo('maintenance')}>Maintenance</button>
	</nav>

	<!-- Main content section -->
	<section>
		<!-- Conditional rendering based on the current page -->
		{#if currentPage === 'home'}
			<h2>Welcome to KFC Management</h2>
			<p>Select a section from the navigation menu to get started.</p>
		{:else if currentPage === 'profile'}
			<h2>Profile</h2>
			<p>Here you can someone's profile.</p>
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
			<p>Here you can manage dashboard.</p>
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
</main>

<style>
	/* Main container styles */
	main {
		text-align: center;
		padding: 1em;
		max-width: 800px;
		margin: 0 auto;
	}

	/* Header styles */
	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 2em;
		font-weight: 100;
	}

	/* Navigation styles */
	nav {
		margin: 2em 0;
	}

	/* Button styles */
	button {
		margin: 0 0.5em;
		padding: 0.5em 1em;
		background-color: #ff3e00;
		color: white;
		border: none;
		border-radius: 4px;
		cursor: pointer;
	}

	/* Button hover effect */
	button:hover {
		background-color: #ff6240;
	}

	/* Content section styles */
	section {
		margin-top: 2em;
	}

	/* Responsive design for larger screens */
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>