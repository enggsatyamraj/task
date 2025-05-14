<script>
	import Router from "svelte-spa-router";
	import Login from "./Login.svelte";
	import Signup from "./Signup.svelte";
	import Dashboard from "./Dashboard.svelte";

	const routes = {
		"/":Dashboard,
		"/login": Login,
		"/signup":Signup
	}

</script>

<Router {routes} />
