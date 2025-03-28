<script setup>
import { ref } from 'vue';
import Button from 'primevue/button';


defineProps({
	currentPageIndex:Number,
	index:Number,
	tabData:Object
})

const size = 35;

</script>

<template>
<button class="tab" :class=" tabData.imageURL == null?
		'unlinked' : 
		currentPageIndex == index? 'selected' : 'not-selected' 
	" :disabled="tabData.imageURL==null">
	<img v-if="tabData.imageURL!=null" :src="tabData.imageURL" :width="size" :height="size">
	<div class="text">{{ tabData.keybind }}</div> 
</button>
</template>

<style>

.selected{
	background-color: #DFDFDF;
	border-color: #000000;

}

.not-selected{
	background-color: #B8B8B8;
	border-color: #4F4F4F;

}

.unlinked{
	background-color: #888888;
	border-color: #2F2F2F;
	border-style: dashed
}

.tab{
	border-width: 3pt;
	width: 11.111111%;
	height: 20;
	position: relative;
}


.text{
	z-index: 2;
	font-weight: bold;
	position: absolute;
	bottom:0%;
	right:0%
}

</style>