<script lang="ts">
	import { Line } from 'svelte-chartjs';
	import { Pie } from 'svelte-chartjs';
	import { data } from '$lib/data.js';

	import {
		Chart as ChartJS,
		Title,
		Tooltip,
		Legend,
		LineElement,
		LinearScale,
		PointElement,
		ArcElement,
		CategoryScale
	} from 'chart.js';
	import { each, isNullOrUndef } from 'chart.js/helpers';

	let year: number = 2023;

	ChartJS.register(
		Title,
		Tooltip,
		Legend,
		LineElement,
		LinearScale,
		ArcElement,
		PointElement,
		CategoryScale
	);
	type ChartData = {
		labels: (string | number)[];
		datasets: {
			label?: string;
			fill?: boolean;
			borderColor?: string;
			data?: number[];
			backgroundColor?: string[];
			hoverBackgroundColor?: string[];
		}[];
	};

	let chart1: ChartData = {
		labels: data.map((element) => element.year),
		datasets: [
			{
				label: 'moški',
				fill: false,
				borderColor: 'rgb(54, 162, 235)',
				data: data.map((element) => element.m)
			},
			{
				label: 'ženske',
				fill: false,
				borderColor: 'rgb(255, 99, 132)',
				data: data.map((element) => element.f)
			},
			{
				label: 'none-binary',
				fill: false,
				borderColor: 'rgb(0, 189, 76)',
				data: [0]
			}
		]
	};

	let chart2: ChartData = {
		labels: ['male', 'female'],
		datasets: [
			{
				backgroundColor: ['rgb(54, 162, 235)', 'rgb(255, 99, 132)'],
				data: [123, 456]
			}
		]
	};
</script>

<div class="container mx-auto">
	<div class="grid grid-cols-2 gap-10 mb-10">
		<div class="border-4 border-violet-200 p-3">
			<h2 class="text-center text-2xl text-violet-700 font-bold">Graf podatkov</h2>
			<Line data={chart1} options={{ responsive: true }} />
		</div>
		<div class="border-4 border-violet-200 p-3">
			<h2 class="text-center text-2xl text-violet-700 font-bold">Tortni graf</h2>
			<input
				class="w-full text-center border-2 border-violet-700"
				type="number"
				bind:value={year}
			/>
			<Pie data={chart2} options={{ responsive: true }} />
		</div>
	</div>
</div>
{#each data as year}
	<p></p>
{/each}
