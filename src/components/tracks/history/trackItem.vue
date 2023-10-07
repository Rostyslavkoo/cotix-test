<template>
	<div class="track">
		<div class="track__info">
			<img :src="track?.imageUrl" v-if="track?.imageUrl" alt="Track Cover" />
			<img src="https://placehold.co/250x250" v-else alt="Track Cover" />
			<span>
				<h2 class="">{{ track?.title }}</h2>
				<p>{{ track?.artist }}</p>
			</span>
		</div>
		<span>
			<p class="track__duration">{{ track?.duration }}</p>
			<p class="track__duration">{{ getTimeAgo }}</p>
		</span>
	</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import moment from 'moment';

export default defineComponent({
	props: {
		track: {
			type: Object,
			default: {},
			require: true,
		},
	},
	computed: {
	// This computed property returns the time elapsed since the track was played, in a human-readable format
		getTimeAgo(): string {
			return moment((this as any).track.time).fromNow();
		},
	},
});
</script>

<style lang="scss" scoped>
.track {
	display: flex;
	align-items: center;
	justify-content: space-between;
	img {
		display: block;
		width: 55px;
		height: 55px;
		flex-shrink: 0;
		border-radius: 5px;
		border: 1px solid rgba(186, 172, 158, 0.23);
	}
	&__info {
		display: flex;
		align-items: center;
		span {
			margin-left: 20px;
		}
		h2 {
			font-family: Montserrat;
			font-size: 13px;
			font-weight: 500;
		}
		p {
			font-size: 11px;
		}
	}
	&__duration {
		font-size: 12px;
	}
}
</style>
