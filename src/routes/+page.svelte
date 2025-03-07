<script>
	import { onMount } from 'svelte';
	import { writable } from 'svelte/store';

	let message = '';
	let messages = writable([]);
	let ws;

	onMount(() => {
		ws = new WebSocket('AQUI NOSSO BACKEND :)');

		ws.onmessage = (event) => {
			messages.update((msgs) => [...msgs, JSON.parse(event.data)]);
		};
	});

	function sendMessage() {
		if (message.trim() !== '') {
			ws.send(JSON.stringify({ text: message, sender: 'User' }));
			message = '';
		}
	}
</script>
