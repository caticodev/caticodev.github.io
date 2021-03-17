<script lang="ts">
	import { Router, Link, Route } from "svelte-routing";
	import Home from "./routes/Home.svelte";
	import Projects from "./routes/Projects.svelte";

	export let url = "";
</script>

<main>
	<Router {url}>
		<Route path="/" component={Home} />
		<Route path="/projects" component={Projects} />
	</Router>
</main>
