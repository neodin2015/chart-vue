<script setup>
const props = defineProps({
	data: {
		type: Array,
		required: true,
		default: () => []
	},
	title: {
		type: String,
		required: false,
		default: ''
	}
})

const maxBarHeight = 150;
const maxValue = Math.max(...props.data.map(item => Math.abs(item.value)));
</script>

<template>
	<div>
		<div class="chart-container">
			<h2 v-if="title">{{ title }}</h2>
			<div class="chart">
				<div v-for="(item, index) in data" :key="index" class="bar-container">
					<div class="value">{{ item.value }}</div>
					<div
						class="bar"
						:style="{
            height: (Math.abs(item.value) / maxValue) * maxBarHeight + 'px',
            backgroundColor: item.value < 0 ? 'green' : 'red',
            bottom: item.value < 0 ? '50%' : 'auto',
            top: item.value >= 0 ? '50%' : 'auto',
            transform: item.value < 0 ? 'translateY(100%)' : 'translateY(-100%)'
          }"
					></div>
					<div class="label">{{ item.label }}</div>
					<div class='divider'></div>
				</div>
			</div>
		</div>
	</div>

</template>

<style scoped>
.chart-container {
	text-align: center;
	overflow-x: auto;
	margin: 20px auto;
	width: 80%;
	border: 1px solid gray;
}

.chart {
	display: flex;
	align-items: center;
	justify-content: flex-start;
	height: 400px;
	padding: 25px 40px;
	position: relative;
}

.chart::before {
	content: '';
	position: absolute;
	background: darkslateblue;
	top: 50%;
	left: 0;
	right: 0;
	height: 1px;
}

.bar-container {
	display: flex;
	flex-direction: column;
	align-items: center;
	height: calc(100% - 80px);
	position: relative;
	margin-right: 50px;
}

.bar {
	width: 20px;
	position: absolute;
	transform-origin: bottom;
}

.value {
	transform: rotate(-90deg) translateX(-49%);
	margin-bottom: 5px;
	position: absolute;
	z-index: 1000;
}

.label {
	transform: rotate(-70deg);
	margin-top: 10px;
	position: absolute;
	bottom: -50px;
}

.divider {
	position: absolute;
	width: 40px;
	height: 1px;
	background-color: darkgray;
	margin-top: 10px;
	bottom: -55px;
}
</style>
