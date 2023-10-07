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
		getStartTime(): string {
			const startTime = moment((this as any).playingTrack?.time);
			const diff = moment.duration(moment().diff(startTime));
			if (diff.asSeconds() > startTime.seconds()) {
				return (this as any).playingTrack?.duration;
			} else {
				return moment.utc(diff.asMilliseconds()).format('HH:mm:ss');
			}
		},
		getBarCodeWidth(): string {
			const startTime = moment((this as any).playingTrack?.time);
			const diff = moment.duration(moment().diff(startTime));

			if (diff.asSeconds() !== 0) {
				const res = (diff.asSeconds() / startTime.seconds()) * 100;
				return `${res}%`;
			} else {
				return '0%';
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
