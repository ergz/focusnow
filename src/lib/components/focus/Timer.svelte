<script lang="ts">
	let current_clock_time = $state("");
	let timer_active = $state(false);
	let focus_time = $state("30");
	let focus_time_counter = $state();
	$effect(() => {
		focus_time_counter = parseInt(focus_time);
	});

	$inspect(focus_time_counter);

	function update_clock() {
		current_clock_time = new Date().toLocaleString();
	}

	function toggle_timer_active() {
		timer_active = !timer_active;
	}

	$effect(() => {
		update_clock();
		const interval = setInterval(update_clock, 1000);

		return () => clearInterval(interval);
	});
</script>

<div class="text-3xl">{current_clock_time}</div>
<div>
	<select class="select select-lg w-full max-w-xs" bind:value={focus_time}>
		<option value="30">30 minutes</option>
		<option value="45">45 minutes</option>
		<option value="60">1 hour</option>
		<option value="120">2 hours</option>
	</select>
	<button class="btn {timer_active ? 'btn-error' : 'btn-success'}" onclick={toggle_timer_active}>
		{timer_active ? "Stop" : "Start"}</button
	>
	<h1>Focus for {focus_time_counter} minutes</h1>
</div>
