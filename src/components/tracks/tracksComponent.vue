<template>
	<div class="my-container">
		<playing-component :playingTrack="playingTrack" />
		<history-Component
			:reversedTrack="reversedTracks"
			v-if="reversedTracks.length"
		/>
	</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

import playingComponent from './playing/playingComponent.vue';
import historyComponent from './history/historyComponent.vue';

import axios from 'axios';
export default defineComponent({
	name: 'tracksComponent',
	components: { playingComponent, historyComponent },
	data() {
		return {
			tracks: [],
			trackUpdateInterval: 0,
		};
	},
	async mounted() {
		await this.getTracks();
		this.trackUpdateInterval = setInterval(() => {
			this.getTracks();
		}, 2000);
	},
	unmounted() {
		clearInterval(this.trackUpdateInterval);
	},
	methods: {
		async getTracks() {
			try {
				const response = await axios.get(
					'https://onair.radioapi.io/thisisgo/go/onair.json'
				);

				this.tracks = response.data.nowplaying;
			} catch (e) {
				alert(e);
			}
		},
	},
	computed: {
		reversedTracks() {
			const historyTracks = [
				...this.tracks.filter(
					(track: { status?: string }) => track.status === 'history'
				),
			];
			return historyTracks;
		},
		playingTrack() {
			const playingTrack = this.tracks.find(
				(track: { status?: string }) => track.status === 'playing'
			);
			return playingTrack ? Object.assign({}, playingTrack) : {};
		},
	},
});
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@100;200;300;400;500;800&family=Montserrat:ital,wght@0,200;0,400;1,600&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@100;200;300;400;500;800&family=Montserrat:ital,wght@0,200;0,900;1,600&display=swap');

body,
html {
	font-family: 'Montserrat', sans-serif;
	background: rgba(249, 249, 249, 0.8);
}
.my-container {
	max-width: 645px;
	width: 100%;
	padding-top: 10%;
	margin: auto;
	display: flex;
	flex-direction: column;
	align-items: center;
}
.d-flex {
	display: flex;
	flex-wrap: wrap;
}
.align-center {
	align-items: center;
}
p {
	color: rgba(0, 0, 0, 0.6);
	font-weight: 400;
}
img {
	-webkit-user-select: none;
	-khtml-user-select: none;
	-moz-user-select: none;
	-o-user-select: none;
	user-select: none;
}
</style>
