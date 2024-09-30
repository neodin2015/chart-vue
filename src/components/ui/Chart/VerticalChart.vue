<script setup>
const props = defineProps({
	quantity: {
		type: Array,
		required: true,
		default: () => [],
	},
	name: {
		type: String,
		required: false,
		default: '',
	},
});

const maxBarHeight = 100;
const maxValue = Math.max(...props.quantity.map(item => Math.abs(item.value)));

const getBarHeight = (value) => (Math.abs(value) / maxValue) * maxBarHeight + 'px';
</script>

<template>
	<div>
		<div class='chart-container'>
			<h2>{{ name }}</h2>
			<div class='chart'>
				<div v-for='(item, index) in quantity' :key='index' class='bar-container'>
					<div
						class='bar'
						:class='{
              negative: item.value < 0,
              positive: item.value >= 0
            }'
						:style='{ height: getBarHeight(item.value) }'
					>
						<div class='value'>{{ item.value }}</div>
					</div>
					<div class='label-container'>
						<div class='label'>
							{{ item.label }}
						</div>
					</div>
				</div>
				<div class='bar-container'></div>
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
	height: 450px;
	padding: 25px 40px;
	position: relative;
}

.bar-container {
	display: flex;
	flex-direction: column;
	align-items: center;
	height: calc(100% - 80px);
	position: relative;
	margin-right: 20px;
	width: 30px;
	flex-shrink: 0;
}

.bar-container:last-child {
	width: 40px;
	margin-right: 0;
	margin-left: -20px;
}

.bar {
	width: 30px;
	position: absolute;
	transform-origin: bottom;
}

.bar.negative {
	background-color: green;
	bottom: 50%;
	transform: translateY(100%);
}

.bar.positive {
	background-color: red;
	top: 50%;
	transform: translateY(-100%);
}

.value {
	transform: rotate(-90deg);
	margin-bottom: 5px;
	z-index: 1000;
	margin-top: -40px;
}

.label-container {
	border-top: 3px solid gray;
	position: absolute;
	bottom: 50px;
	width: 30px;
}

.label {
	left: 0;
	top: 0;
	position: absolute;
	transform-origin: top;
	transform: rotate(-80deg) translate(-65%, -160%);
	white-space: nowrap;
}
</style>
