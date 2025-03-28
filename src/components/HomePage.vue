<script setup>
import Toolbar from 'primevue/toolbar';
import Button from 'primevue/button';
import { ref } from "vue";
import Dialog from 'primevue/dialog';
import InputText from 'primevue/inputtext';
import Select from 'primevue/select';
import ImageButton from './ImageButton.vue';
import File from './File.vue';
import { IconField, InputIcon } from 'primevue';

const visible = ref(false);
const keybindOptions = ref([])

const data = ref({})

defineProps({
	tabs:Array,
	scriptIndex:Array
});

function refresh(tabs){
	data.value = {};
	keybindOptions.value = [];
	tabs.forEach((element,index) => {
		if(index != 0) keybindOptions.value.push({
				name: element.keybind,
				code: index
			})
	});
}

function save(tabs, scriptIndex){
	const index = data.value.keybind.code
	tabs[index].imageURL = data.value.image;
	tabs[index].name = data.value.name;
	tabs[index].link = "scriptDoc.jpg";
	scriptIndex[0]=index;
}

</script>

<template>
	<div class="home-bar">
		<Toolbar>
			<template #start> 
				<ImageButton src="arrow.svg" height="30px" rotation="180deg"/>
				<ImageButton src="arrow.svg" height="30px"/>

			</template>
			<template #center>
				<IconField>
					<InputIcon>
						<i class="pi pi-search" />
					</InputIcon>
					<InputText placeholder="Search" />
				</IconField>
			</template>
			<template #end> 
				<ImageButton disabled src="delete.png" height="30px"/>
				<ImageButton class="enabled" src="add.svg" height="30px" @click="visible=true; refresh(tabs)"/>

			</template>
		</Toolbar>

        <Dialog v-model:visible="visible" modal header="Add Shortcut" :style="{ width: '25rem' }">
            <div class="grid">
                <label  for="name">Shortuct Name</label>
                <InputText id="name" v-model="data.name" autocomplete="off" />
                
				<label for="link">Link</label>
                <InputText id="link" v-model="data.link" autocomplete="off" />

				<p>Icon</p>
				<div class="right-box">
					<button class="dialog-button enabled" @click="data.image='script.png'" ><img src="/browse.svg" height=35px></img></button>
					<img :src="data.image? data.image : 'Placeholder.svg'" height="35px" style="background-color: gray;">

				</div>

				<p>Link</p>
				<div class="card flex justify-center">
					<Select id="keybind" v-model="data.keybind" :options="keybindOptions" optionLabel="name" placeholder="Select a Keybind" class="w-full md:w-56 keybind-drop" />
				</div>
                <Button type="button" label="Cancel" severity="secondary" @click="visible = false"></Button>
                <Button type="button" label="Save" @click="visible = false; save(tabs, scriptIndex)"></Button>
            </div>
        </Dialog>
	</div>
	<div style="padding-top: 6rem; display: grid; width: 100%; grid-template-columns: auto auto auto auto auto;">
		<File icon="folder.svg" name="maps"/>
		<File icon="table.png" name="Tables.sc"/>
		<File v-if="scriptIndex[0] >0" icon="script.png" :name="tabs[scriptIndex[0]].name + '.sc'"/>


	</div>
</template>


<style>

InputText{
	border-width: 1px;
}

.keybind-drop{
	width: 100%;
}


.home-bar{
	width: 100%;
	left:0%;
	margin: auto;
	position:absolute;
	padding-top: 20px;
}

.right-box{
	display: flex;
	justify-content: end;
}

.grid{
  display: grid;
  grid-template-columns: auto auto;
  row-gap: 10px;
  column-gap: 10px;
  align-items:right;
}

.bar-button, .dialog-button {
	padding: 0%;
	background-color: transparent;
	border-color: transparent;
}

.dialog-button{
	margin-right: 10px;
}

.bar-button {
	margin-left: 10px;
}

.title{
	font-weight: bold;
	padding-left: 10px;
}
</style>