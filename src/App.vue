<script setup>
import elementInventory from "./components/element-inventory.vue";
import detailsInfo from "@/components/details-info.vue";
import closeIcon from "@/components/icon/close.vue";
import { ref, reactive, computed } from "vue";

const window = ref(false);

const data = reactive({ param: { color: "", quantity: 0 } });

// interface boards {

//   color: string;
//   quantity: number[];
// }

let board = ref(Array(25).fill({ color: null, quantity: 0 }));
board.value[0] = {
	color: "#394932",
	quantity: 21
};
board.value[7] = {
	color: "#943",
	quantity: 2
};
board.value[10] = {
	color: "#923143",
	quantity: 2
};
function hasDraggable(color, quantity) {
	if (color !== "" && quantity !== 0) {
		return true;
	}
	return false;
}
function name(params) {
	if (params.color != "" && params.quantity != "") {
		window.value = true;
		data.param = params;
		return data;
	}
}

const draggedItem = ref(null);

const dragStart = (event, index) => {
	draggedItem.value = index;
};
const drop = (event, index) => {
	if (draggedItem.value !== null) {
		if (draggedItem.value !== null) {
			const item = board.value[draggedItem.value];
			const itemPosition = board.value[index];

			board.value.splice(draggedItem.value, 1);

			board.value.splice(index, 0, item);

			draggedItem.value = null;
		}
	}
};
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
					v-for="(i, key) in board"
					:key="key"
					@click-by="(n) => name(n)"
					:color="i.color"
					:quantity="i.quantity"
					:draggable="hasDraggable(i.color, i.quantity)"
					@dragstart="dragStart($event, key)"
					@drop="drop($event, key)"
					@dragover.prevent
				>
				</elementInventory>
			</ul>
		</div>
		<div class="inventory__message">
			<div class="hide"></div>
			<div class="position"><closeIcon></closeIcon></div>
		</div>
	</div>
</template>
