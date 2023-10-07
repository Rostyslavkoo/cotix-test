<template>
	<div class="progress-bar">
		<div class="progress-bar__wrapper">
			<div :style="{ width: getBarCodeWidth }"></div>
		</div>
		<div class="progress-bar__times">
			<p>{{ getStartTime }}</p>

			<p>{{ playingTrack?.duration || '00:00:00' }}</p>
		</div>
	</div>
</template>

<script lang="ts">
import moment from 'moment';

import { defineComponent } from 'vue';

export default defineComponent({
	name: 'progress Bar',
	props: {
		playingTrack: {
			type: Object,
			default: {},
			required: true,
		},
	},
	computed: {
		// This computed property returns the start time of the playing track in the format "HH:mm:ss"
		getStartTime(): string {
			const startTime = moment((this as any).playingTrack?.time);
			const diff = moment.duration(moment().diff(startTime));
			return moment.utc(diff.asMilliseconds()).format('HH:mm:ss');
		},
		// This computed property returns the width of the progress bar as a percentage of the total duration of the playing track
		getBarCodeWidth(): string {
			const startTime = moment((this as any).playingTrack?.time);
			const diff = moment.duration(moment().diff(startTime));
			return `${(diff.asSeconds() / this.getDurationInSeconds) * 100}%`;
		},
		// This computed property returns the duration of the playing track in seconds
		getDurationInSeconds() {
			if ('duration' in this.playingTrack) {
				const durationArray = (this as any).playingTrack?.duration.split(':');

				const minutes = parseInt(durationArray[1], 10);
				const seconds = parseInt(durationArray[2], 10);
				return minutes * 60 + seconds;
			} else {
				return 0;
			}
		},
	},
});
</script>

<style lang="scss" scoped>
.progress-bar {
	&__wrapper {
		cursor: pointer;
		width: 100%;
		height: 7px;
		border-radius: 7px;
		// border: .1px solid #e3e3e3;
		background: #fff;
		box-shadow: 0px 0px 3px 0px rgba(0, 0, 0, 0.2);
		div {
			width: 0;
			max-width: 100%;
			height: 5px;
			border-radius: 7px;
			border: 0.5px solid #e96d6d;
			background: rgba(233, 109, 109, 0.9);
		}
	}
	&__times {
		display: flex;
		justify-content: space-between;
		align-items: center;
		p {
			margin-top: 3px;
			font-size: 12px;
		}
	}
}
</style>

function defineComponent(arg0: { name: string; props: { playingTrack: { type:
ObjectConstructor; default: {}; required: boolean; }; }; computed: {
getStartTime(): string; getBarCodeWidth(): string; }; }) { throw new
Error('Function not implemented.'); }
