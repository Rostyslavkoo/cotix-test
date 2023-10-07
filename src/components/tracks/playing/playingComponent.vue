<template>
	<div class="track d-flex align-center">
		<div
			class="track__img"
			@click="openAlbumURL(playingTrack.iTunesTrackUrl)"
			target="_blank"
		>
			<img
				:src="playingTrack?.imageUrl"
				v-if="playingTrack?.imageUrl"
				alt="Track Cover"
				width="250px"
				height="250px"
			/>
			<img src="https://placehold.co/250x250" v-else alt="Placeholder" />
		</div>
		<div class="track__info">
			<h2 class="">{{ playingTrack?.title || '--' }}</h2>
			<p>{{ playingTrack?.artist || '--' }}</p>
			<progress-bar :playingTrack="playingTrack" />
		</div>
	</div>
</template>

<script lang="ts">
import progressBar from './progressBar.vue';
import { defineComponent } from 'vue';

export default defineComponent({
	components: { progressBar },
	name: 'Playing Component',
	props: {
		playingTrack: {
			type: Object,
			default: {},
			required: true,
		},
	},
	methods: {
		openAlbumURL(iTunesTrackUrl: string) {
			window.open(iTunesTrackUrl, '_blank');
		},
	},
});
</script>

<style lang="scss" scoped>
.track {
	min-height: 250px;
	width: 100%;
	padding: 0;
	justify-content: center;
	&__img {
		position: relative;
		&:hover {
			cursor: pointer;
			transition: 0.25s ease;
			&::after {
				position: absolute;
				top: 0;
				left: 0;
				content: '';
				display: block;
				z-index: 100;
				width: 100%;
				height: 100%;
				transition: 0.25s ease;

				background: #ffffff1e;
			}
		}
		&:active {
			transform: scale(0.95);
		}
		img {
			max-height: 250px;
			height: 100%;
			width: 250px;
			border-radius: 10px;
			border: thin solid rgba(7, 7, 7, 0.1);
			box-shadow: 0px 1px 14px 2px rgba(92, 92, 92, 0.189);
			object-fit: cover;
			margin: 0 30px 0 30px;
			display: block;
		}
	}
	&__info {
		width: 330px;
		h2 {
			margin-bottom: 0;
			font-size: 20px;
			font-weight: 900;
		}
		p {
			margin-top: 5px;
			margin-bottom: 35px;
			font-size: 14px;
		}
	}
}
</style>
