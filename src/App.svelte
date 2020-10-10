<script>
	// Component
	import Navbar from './Navbar.svelte';
	import ExpensesList from './ExpensesList.svelte';
	// Data
	import expensesData from './expenses';
	// Variables
	let expenses = [...expensesData];
	console.log(expenses)
</script>

<Navbar />
<main class="content">
	<ExpensesList {expenses} />
</main>
