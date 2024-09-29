<script setup>
import VerticalChart from './components/ui/Chart/VerticalChart.vue';
import { onMounted, ref } from 'vue';

const charts = ref([]);
onMounted(async () => {
	const data = await fetch('/api/diagram-data-second-task.json').then((res) => res.json());
	charts.value = Object.keys(data).
		map((key) => ({
			title: key,
			dataset: data[key].map(_item => ({
				label: _item.name,
				value: _item.quantity,
			})),
		}));
	console.log(charts.value);
});
</script>

<template>
	<VerticalChart v-for='chart in charts' :data='chart.dataset' :title='chart.title' />
</template>

<style scoped>
.logo {
	height: 6em;
	padding: 1.5em;
	will-change: filter;
	transition: filter 300ms;
}

.logo:hover {
	filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
	filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
