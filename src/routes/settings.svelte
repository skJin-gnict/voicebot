<script lang="ts">
	import { debugMode } from '$lib/stores/config';
	import { onDestroy } from 'svelte';

	const interval = setInterval(() => {
		console.log($debugMode);
	}, 5000);

	onDestroy(() => {
		console.log('settings.svelte destroyed');
		clearInterval(interval);
	});
</script>

<h1>General</h1>
<div>
	<input type="checkbox" name="debug-mode" id="debug-mode" bind:checked={$debugMode} />
	<label for="debug-mode">Debug mode</label>
</div>

<h2>WebRTC settings</h2>

<form action="/settings" id="webrtc" method="POST">
	<div class="option">
		<input name="use-datachannel" id="use-datachannel" type="checkbox" />
		<label for="use-datachannel">Use datachannel</label>
		<select name="datachannel-parameters" id="datachannel-parameters" form="webrtc">
			<option value={{ ordered: true }}>Ordered, reliable</option>
			<option value={{ ordered: false, maxRetransmits: 0 }}> Unordered, no retransmissions </option>
			<option value={{ ordered: false, maxPacketLifetime: 500 }}>
				Unordered, 500ms lifetime
			</option>
		</select>
	</div>
	<div class="option">
		<input name="use-audio" id="use-audio" type="checkbox" />
		<label for="use-audio">Use audio</label>
		<select name="audio-codec" id="audio-codec" form="webrtc">
			<option value="default">Default codecs</option>
			<option value="opus/48000/2" selected>Opus</option>
			<option value="PCMU/8000">PCMU</option>
			<option value="PCMA/8000">PCMA</option>
		</select>
	</div>
	<div class="option">
		<input name="use-video" id="use-video" checked="checked" type="checkbox" />
		<label for="use-video">Use video</label>
		<select name="video-resolution" id="video-resolution" form="webrtc">
			<option value="">Default resolution</option>
			<option value="320x240" selected>320x240</option>
			<option value="640x480">640x480</option>
			<option value="960x540">960x540</option>
			<option value="1280x720">1280x720</option>
		</select>
		<select name="video-transform" id="video-transform" form="webrtc">
			<option value="none" selected>No transform</option>
			<option value="edges">Edge detection</option>
			<option value="cartoon">Cartoon effect</option>
			<option value="rotate">Rotate</option>
		</select>
		<select name="video-codec" id="video-codec" form="webrtc">
			<option value="default">Default codecs</option>
			<option value="VP8/90000">VP8</option>
			<option value="H264/90000" selected>H264</option>
		</select>
	</div>
	<div class="option">
		<input name="use-stun" id="use-stun" type="checkbox" checked="checked" />
		<label for="use-stun">Use STUN server</label>
	</div>

	<br />

	<button id="update">Update</button>
</form>
