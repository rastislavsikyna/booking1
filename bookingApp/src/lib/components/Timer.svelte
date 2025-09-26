

<script>
	let time = $state(new Date());

	setInterval(() => {
		time = new Date();
	}, 1000);
</script>

<p>{time.getHours()}:{time.getMinutes()}:{time.getSeconds()}</p>

