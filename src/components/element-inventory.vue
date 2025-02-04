<template>
	<li class="board__item item" @click="$emit('clickBy', { color, quantity })">
		<div class="item__content">
			<!-- <img :src="color" alt="" /> -->
		</div>
		<p class="item__quantity" v-if="quantity">{{ quantity }}</p>
	</li>
</template>

<script setup lang="ts">
import { ref } from "vue";

defineProps<{
	color?: string;
	quantity?: number;
}>();
</script>

<style lang="scss">
.item {
	cursor: pointer;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	&__content {
		margin: 10px;
		background: v-bind(color);
		opacity: 0.75;
		box-shadow: -10px 10px 1.4px v-bind(color);
		width: 48px;
		height: 48px;
		align-self: center;
	}
	&__quantity {
		align-self: end;
		border: 2px solid rgba(77, 77, 77, 1);
		border-top-left-radius: 6px;
		width: 16px;
		text-align: center;
		height: 16px;
		color: white;
	}
	p {
		padding: 0;
		margin: 0;
	}
}
</style>
