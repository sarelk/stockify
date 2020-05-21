<template>
  <div>
    <zingchart ref="myChart" 
               :data="chartConfig" 
               @label_click="changeDate"
               :width="700">
    </zingchart>
  </div>
</template>

<script>
import zingchartVue from 'zingchart-vue';
import {closes, dates, volumes} from '../data';
export default {
  name: 'SingleStock',
  components: {
    zingchart: zingchartVue,
  },
  computed: {
    closeConfig() {
      return {
        
          type: 'area',
          backgroundColor: '#333',
          height: '420px',
          x: '0px',
          y: '0px',
          title: {
            text: 'GOOG',
            align: 'left',
            fontColor: '#fff',
            fontFamily: 'Open Sans',
            fontSize: '30px',
            offsetX: '10px'
          },
          plot: {
            marker: {
              visible: false
            }
          },
          plotarea: {
            margin: '60 50 40 50'
          },
          scaleX: {
            values: this.dates,
            guide: {
              lineColor: '#444',
              lineStyle: 'solid',
              visible: true
            },
            item: {
              fontColor: '#ddd',
              fontFamily: 'Open Sans'
            },
            transform: {
              type: 'date',
              all: '%m/%d/%y'
            },
            zooming: {
              shared: true
            }
          },
          scaleY: {
            values: '450:810:20',
            guide: {
              lineColor: '#444',
              lineStyle: 'solid',
              visible: true
            },
            item: {
              fontColor: '#ddd',
              fontFamily: 'Open Sans'
            }
          },
          crosshairX: {
            plotLabel: {
              text: 'Close: %v',
              backgroundColor: '#bbb',
              fontColor: '#222',
              fontFamily: 'Open Sans',
              y: '0px'
            },
            scaleLabel: {
              backgroundColor: '#bbb',
              fontColor: '#222',
              fontFamily: 'Open Sans'
            },
            shared: true
          },
          tooltip: {
            text: 'Close: %v',
            backgroundColor: '#BBB',
            borderColor: 'transparent'
          },
          labels: [
            {
              id: '1W',
              text: '1W',
              cursor: 'hand',
              fontColor: (this.current === '1W') ? '#FFF' : '#777',
              fontFamily: 'Open Sans',
              fontSize: '16px',
              x: '490px',
              y: '10px'
            },
            {
              id: '1M',
              text: '1M',
              cursor: 'hand',
              fontColor: (this.current === '1M') ? '#FFF' : '#777',
              fontFamily: 'Open Sans',
              fontSize: '16px',
              x: '530px',
              y: '10px'
            },
            {
              id: '6M',
              text: '6M',
              cursor: 'hand',
              fontColor: (this.current === '6M') ? '#FFF' : '#777',
              fontFamily: 'Open Sans',
              fontSize: '16px',
              x: '570px',
              y: '10px'
            },
            {
              id: '1Y',
              text: '1Y',
              cursor: 'hand',
              fontColor: (this.current === '1Y') ? '#FFF' : '#777',
              fontFamily: 'Open Sans',
              fontSize: '16px',
              x: '610px',
              y: '10px'
            },
            {
              id: '2Y',
              text: '2Y',
              cursor: 'hand',
              fontColor: (this.current === '2Y') ? '#FFF' : '#777',
              fontFamily: 'Open Sans',
              fontSize: '16px',
              x: '650px',
              y: '10px'
            }
          ],
          zoom: {
            shared: true
          },
          series: [
            {
              values: this.closes,
              backgroundColor: '#909090 #313131',
              lineColor: '#fff',
              lineWidth: '1px'
            }
          ]
        
      }
    },
    volumeConfig() {
      return {
        type: 'bar',
        backgroundColor: '#333',
        height: '80px',
        x: '0px',
        y: '400px',
        plotarea: {
          margin: '20 50 30 50'
        },
        scaleX: {
          visible: false,
          zooming: true
        },
        scaleY: {
          visible: false
        },
        crosshairX: {
          plotLabel: {
            text: 'Volume: %v',
            backgroundColor: '#BBB',
            fontFamily: 'Open Sans',
            y: '0px'
          },
          scaleLabel: {
            visible: false
          },
          shared: true
        },
        tooltip: {
          text: 'Volume: %v',
          borderColor: 'transparent',
          fontFamily: 'Open Sans',
          visible: false
        },
        source: {
          text: 'nasdaq.com',
          fontColor: '#ddd',
          fontFamily: 'Open Sans'
        },
        zoom: {
          shared: true
        },
        series: [
          {
            text: 'Volume',
            values: this.volumes,
            backgroundColor: '#bbb'
          }
        ]
      };
    },
    dates() {
      return dates.slice(dates.length - this.cut);
    },
    closes() {
      return closes.slice(closes.length - this.cut);
    },
    volumes() {
      return volumes.slice(volumes.length - this.cut);
    },
    cut() {
      let cut = 0;
      switch (this.current) {
        case '1W':
          cut = 5;
          break;
        case '1M':
          cut = 20;
          break;
        case '6M':
          cut = 130;
          break;
        case '1Y':
          cut = 260;
          break;
        default:
          cut = dates.length;
          break;
      }
      return cut;
    },
    chartConfig() {
      return {
        graphset: [
          this.closeConfig,
          this.volumeConfig,
        ]
      }
    }
      
  },
  data(){
    return {
      current: '2Y',
    }
  },
  mounted() {
    
  },
  methods: {
    changeDate(e) {
      this.current = e.labelid;
    }
  },
}
</script>
