<script>
    import ApexCharts from 'apexcharts'
    import {onMount, onDestroy} from 'svelte'

    export let text

    const levels = [820, 681, 1698]
    const userLevels = [505, 269, 155]
    const difference = userLevels.map((userN, i) => levels[i] - userN)

    const options = {
        title: {
            text: 'Level',
            align: 'left'
        },
        chart: {
            type: 'bar',
            width: 800,
            height: 500,
            stacked: true,
            toolbar: {
                show: false
            },
            parentHeightOffset: 0,
        },
        colors: ['#a9d4a5', '#e7e7e7'],
        legend: {
            // 			show: false,
            position: 'top',
            onItemHover: {
                highlightDataSeries: false
            },
        },
        xaxis: {
            categories: ['A1', 'A2', 'B1'],
            labels:	{
                style: {
                    fontWeight: 800
                }
            }
        },
        dataLabels: {
            enabled: true,
            enabledOnSeries: [0],
            formatter: function(value, opt) {
                const { seriesIndex, dataPointIndex, w } = opt
                if(seriesIndex === 0) {
                    return Math.round(userLevels[dataPointIndex] / levels[dataPointIndex] * 100) + '%'
                }
            }
        },
        tooltip: {
            x: {
                show: false
            },
            y: {
                formatter: function(value, opt) {
                    const {dataPointIndex} = opt
                    return `${value} / ${levels[dataPointIndex]}`
                }
            },
            shared: true,
            intersect: false,
            inverseOrder: true,
        },
        states: {
            hover: {
                filter: {
                    type: 'none',
                }
            },
        },
    };

    let series = [
        {
            name: 'Saved',
            data: userLevels
        },
        {
            name: 'All',
            data: difference
        }
    ]

    options.series = series

    let container, chart

    onMount(() => {
        chart = new ApexCharts(container, options);
        chart.render();
    })

    onDestroy(() => {
        chart = undefined
    })


</script>

<input type="text" bind:value={text} /> <button on:click>click > log</button>

<div class="chart-container" bind:this={container}></div>

<style>
    div {
        width: 100%;
        padding: 2rem;
        margin: .5rem;
        background: white;
        border-radius: 6px;
    }
</style>