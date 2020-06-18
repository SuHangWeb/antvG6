<template>
  <div ref="ringChart" class="ringChart"></div>
</template>

<script>
  import echarts from 'echarts'
  export default {
    name: "Ring",
    props: {
      //颜色
      color: {
        type: String,
        default () {
          return 'red'
        }
      },
      //数据
      data: {
        type: Object,
        default () {
          return {}
        }
      }
    },
    data () {
      return {
      }
    },
    mounted(){
      
      const option = {
        legend: {
            orient: 'vertical',
            left: 'center',
            top: '10%',
            selectedMode:false,
            icon:'none',
            formatter: [
                `{a|${this.data.text}}{b|/${this.data.subtext}}`,
            ].join('\n'),
            textStyle: {
                rich: {
                    a: {
                        color: this.color,
                        textShadowColor:this.color,
                        textShadowBlur:2,
                        fontSize: 14
                    },
                    b: {
                        color: '#DCDCDC',
                        fontSize: 12,
                    },
                }
            }
        },
        title: {
            text: `${parseFloat(this.data.value)}%`,
            textStyle: {
                color: this.color,
                textShadowColor:this.color,
                textShadowBlur:2,
                fontSize: 22
            },
            left: 'center',
            top: '80%'
          },
        angleAxis: {
            max: 100,
            show: false,
        },
        radiusAxis: {
            type: 'category',
            show: true,
            axisLabel: {
                show: false,
            },
            axisLine: {
                show: false,

            },
            axisTick: {
                show: false
            },
        },
        polar: {
            radius: '75%',
            center: ['50%', '50%'],
        },
        series: [{
            type: 'bar',
            // 圆角
            // roundCap: true,
            barWidth: 40,
            showBackground: true,
            backgroundStyle: {
                color: "rgba(219,219,219,0.3)"
            },
            data: [parseFloat(this.data.value)],
            coordinateSystem: 'polar',
            name: `${parseFloat(this.data.value)}`,
            label: {
                show: true,
            },
            itemStyle: {
                normal: {
                    opacity: 1,
                    color: this.color,
                }
            },
        }],
      }
      const chartObj = echarts.init(this.$refs.ringChart);
      chartObj.setOption(option)
    }
  }
</script>
<style lang="scss" scoped>
  .ringChart{
    width: 100%;
    height: 100%;
  }
</style>