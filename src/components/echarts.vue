<template>
    <div class="echarts-demo">
        <scroll class="wrap">
            <div class="contents">
                <div class="myCharts" ref="myCharts" style="width: 300; height: 600px"></div>
            </div>
        </scroll>
    </div>
</template>

<script>
    import Echarts from 'echarts'
    import Scroll from './scroll'
    export default {
        data(){
            return {

            }
        },
        components: {
            Scroll
        },
        mounted(){
            setTimeout(() => {
                this.init()
            }, 20);
        },
        methods: {
            init(){
                let echartsEl = this.$refs.myCharts
                let myCharts = Echarts.init(echartsEl)
                myCharts.setOption(
                    {
                        title: {
                            text: "Test",
                            subtext: ""
                        },
                        tooltip: {
                            trigger: "axis",
                            show: true,
                            axisPointer: {
                                type: "shadow"
                            },
                        formatter: '{b0}: {c0}<br />{b1}: {c1}'
                        },
                        dataZoom: [{
                            type: 'inside',
                            startValue:0,
                            endValue: 5,
                            zoomLock: true,
                            orient: 'horizontal'
                        }],
                        toolbox: {
                            show: true,
                            feature: {
                                mark: {
                                    show: true
                                },
                                dataView: {
                                    show: true,
                                    readOnly: true
                                },
                                magicType: {
                                    show: false,
                                    type: ["line", "bar"]
                                },
                                restore: {
                                    show: true
                                },
                                saveAsImage: {
                                    show: true
                                },
                                dataZoom: {
                                    show: true
                                }
                            }
                        },
                        xAxis: [
                            {
                                type: "category",
                                data: ["早饭前", "早饭后", "午饭前", "午饭后", "晚饭前", "晚饭后","早饭前", "早饭后", "午饭前", "午饭后", "晚饭前", "晚饭后"],
                                axisLine: {
                                    show: true,
                                    lineStyle: {
                                        type: "dotted",
                                        width: 1
                                    }
                                },
                                axisLabel: {
                                    show: true
                                },
                                axisTick: {
                                    show: false
                                },
                                splitLine: {
                                    show: false,
                                    lineStyle: {
                                        type: "dashed"
                                    }
                                },
                                boundaryGap: true
                            }
                        ],
                        yAxis: [
                            {
                                type: "value",
                                axisLine: {
                                    show: false,
                                    lineStyle: {
                                        type: "dashed",
                                        width: 1
                                    }
                                },
                                axisLabel: {
                                    show: false
                                },
                                axisTick: {
                                    show: false,
                                    lineStyle: {
                                        color: "rgb(255, 255, 86)"
                                    }
                                },
                                position: "left",
                                scale: true,
                                splitLine: {
                                    show: true
                                }
                            }
                        ],
                        series: [
                            {
                                name: "血糖值",
                                type: "bar",
                                data: [2, 4.9, 7, 23.2, 25.6, 76.7, 135.6, 162.2, 32.6, 20, 6.4, 3.3],
                                markPoint: {
                                    data: [
                                        {
                                            type: "max",
                                            name: "最大值"
                                        },
                                        {
                                            type: "min",
                                            name: "最小值"
                                        }
                                    ]
                                },
                                markLine: {
                                    data: [
                                        {
                                            type: "average",
                                            name: "平均值"
                                        }
                                    ]
                                },
                                itemStyle: {
                                    normal: {
                                        color: "rgb(191, 0, 0)",
                                        label: {
                                            position: "top",
                                            show: false,
                                            textStyle: {
                                                color: "rgb(0, 0, 0)",
                                                fontSize: 16
                                            }
                                        },
                                        barBorderRadius: [8, 8, 0, 0]
                                    }
                                },
                                barCategoryGap: "38%",
                                stack: ""
                            }
                        ],
                        backgroundColor: "rgb(255, 255, 255)",
                        grid: {
                            x2: 40,
                            y2: 28,
                            borderWidth: 0,
                            y: 40,
                            x: 40
                        }
                    }
                )
                var timer
                myCharts.on('datazoom', function (params) {
                    var option = myCharts.getOption()
                    console.log(option.dataZoom[0].startValue, option.dataZoom[0].endValue);
                    if (option.dataZoom[0].startValue == 4){
                        console.log('--------------------')
                    }
                });
            },

        }
    }
</script>
<style>
    .wrap {
        width: 700px;
        overflow: hidden;
    }
    .contents{
        width: 700px;
    }
</style>
