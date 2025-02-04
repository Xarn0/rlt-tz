<script setup lang="ts">
import elementInventory from "./components/element-inventory.vue";
import detailsInfo from "@/components/details-info.vue";
import closeIcon from "@/components/icon/close.vue";
import { ref, reactive } from "vue";

const window = ref(false);
const data = reactive({ param: { color: "", quantity: 0 } });

function name(params: any) {
	if (params.color != "" && params.quantity != "") {
		window.value = true;
		data.param = params;
		return data;
	}
}
</script>

<template>
	<div class="container inventory">
		<div class="inventory__profile">
			<div class="inventory__image">
				<img src="./assets/img/Blur.png" alt="" />
			</div>
			<ul>
				<li class="hide"></li>
				<li class="hide"></li>
				<li class="hide"></li>
				<li class="hide"></li>
				<li class="hide"></li>
				<li class="hide"></li>
			</ul>
		</div>
		<div class="inventory__list">
			<detailsInfo
				:window="window"
				:data="data.param"
				@close-window="
					() => {
						window = false;
					}
				"
			></detailsInfo>
			<ul class="board">
				<elementInventory
					@click-by="(n) => name(n)"
					color="#7faa65"
					:quantity="21"
				></elementInventory>
				<elementInventory
					@click-by="(n) => name(n)"
					color="#049"
					:quantity="5"
				></elementInventory>
				<elementInventory
					@click-by="(n) => name(n)"
					color="#943"
					:quantity="7"
				></elementInventory>

				<li class="board__item" v-for="i in 22" key="i"></li>
			</ul>
		</div>
		<div class="inventory__message">
			<div class="hide"></div>
			<div class="position"><closeIcon></closeIcon></div>
		</div>
	</div>
</template>
