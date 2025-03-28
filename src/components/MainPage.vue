<script setup>
import Tab from '@/components/Tab.vue';
import { ref, reactive } from 'vue';
import TopBar from './TopBar.vue';
import HomePage from './HomePage.vue';
import ScrollPanel from 'primevue/scrollpanel';


const pageState = reactive({
	currentPageIndex: 0,
	scriptIndex: ref([-1]),
	tabs:[
		{
			imageURL:"Home.png",
			keybind: "ESC",
			name:"Home"
		},
		{
			imageURL:"table.png",
			name:"Table",
			link:"tables.jpg"
		},
		{},
		{},
		{},
		{},
		{},
		{},
		{}
	]
})

for (let index = 0; index < pageState.tabs.length; index++) {
	const element = pageState.tabs[index];
	if(element.keybind) continue;
	element.keybind = "F"+index;
}

</script>

<template>
	<TopBar :pageState="pageState" style="z-index: 10;" />
	<HomePage v-if="pageState.currentPageIndex==0" :tabs="pageState.tabs" :script-index="pageState.scriptIndex"/>
	<ScrollPanel v-else style="width: 100%; height: 50rem; padding: 0%; padding-top: 30px; left: 0; z-index: -10;">
		<img :src="pageState.tabs[pageState.currentPageIndex].link" width="auto"/>
	</ScrollPanel>
	<div class="flex-container" style="z-index: 10;">
		<tab v-for="(tab, index) in pageState.tabs" :tabData="tab" :index="index" :currentPageIndex="pageState.currentPageIndex" @click="pageState.currentPageIndex=index"/>
	</div>
</template>

<style>
.flex-container {
	display: flex;
	bottom: 0%;
	position:fixed;
	left:0%;
	margin: auto;
	width: 100%;
}
.flex-container > tab {
	padding: 100%;
}
</style>