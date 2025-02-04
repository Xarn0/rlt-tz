<script setup>
import { ref } from "vue";
import closeIcon from "@/components/icon/close.vue";
defineProps({
	window: {
		type: Boolean
	},
	data: {
		type: Object,
		default: {}
	}
});

let btnActive = ref(false);
</script>

<template>
	<div
		class="inventory__details details"
		:class="{ active: window }"
		v-if="window"
	>
		<div class="details__close" @click="$emit('closeWindow')">
			<closeIcon></closeIcon>
		</div>
		<div class="details__img">
			<span :style="{ background: data.color }"></span>
			<span :style="{ background: data.color }"></span>
		</div>
		<div class="details__text">
			<h4 class="hide"></h4>
			<p class="hide"></p>
			<p class="hide"></p>
			<p class="hide"></p>
			<p class="hide"></p>
		</div>
		<div class="details__btns">
			<button
				class="details__btns-delete"
				v-if="!btnActive"
				@click="btnActive = true"
			>
				Удалить предмет
			</button>
			<div class="dialog" v-else>
				<input type="number" placeholder="Введите количество" />
				<div class="gialog__btns">
					<button
						type="button"
						class="details__btns-cansel"
						@click="btnActive = false"
					>
						Отмена
					</button>
					<button type="button" class="details__btns-delete">
						Подтвердить
					</button>
				</div>
			</div>
		</div>
	</div>
</template>

<style lang="scss">
.details {
	&__img {
		&::after {
			background-color: inherit;
		}
		&::before {
			background-color: inherit;
		}
	}
}
</style>
