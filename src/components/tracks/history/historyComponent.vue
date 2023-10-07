<template>
	<div class="history__wrapper">
		<div class="h2">History</div>
		<div class="history__list">
			<div v-for="(track, index) in reversedTrack" :key="index">
				<track-item :track="track" />
				<div class="my-hr" v-if="index + 1 !== reversedTrack.length"></div>
			</div>
		</div>
	</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import trackItem from './trackItem.vue';
export default defineComponent({
	components: { trackItem },
	props: {
		reversedTrack: {
			type: Object,
			default: {},
			required: true,
		},
	},
});
</script>

<style lang="scss" scoped>
.history {
	&__wrapper {
		margin-top: 50px;
		padding: 30px 40px;
		width: 100%;
		border-radius: 5px;
		background: rgba(249, 249, 249, 0.8);
		box-shadow: 0px 1px 1px 2px rgba(0, 0, 0, 0.04);
	}
	&__list {
		margin-top: 30px;
	}
}
.my-hr {
	width: 100%;
	height: 1px;
	background: rgba(221, 220, 220, 0.95);
	margin: 6px 0;
}
</style>
