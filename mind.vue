<template>
  <div id="mind"></div>
</template>

<script>
  import G6 from '@antv/g6';
  export default {
    name: "Mind",
    props: {
      // 数据
      data: {
        type: Object,
        default () {
          return {}
        }
      },
      //高度
      height:{
        type: Number,
        default () {
          return 0
        }
      }
    },
    data () {
      return {
        
      }
    },
     mounted() {
      const vm = this;
      const fontSize = 12;
      // 自定义节点
      G6.registerNode('line', {
        draw: (cfg, group) => {
          const width = cfg.label.length * 10;
          const rect = group.addShape('rect', {
            attrs: {
              x: 0,
              y: -10,
              ...cfg.style,
              width,
              height: 20,
              lineWidth: 0,
              opacity: 0
            },
            name: 'rect-shape',
            draggable: true
          });
          const label = group.addShape('text', {
            attrs: {
              text: cfg.label,
              fill: '#fff',
              fontSize,
              x: 0,
              y: -5
            },
            name: 'label-shape',
            draggable: true
          });
          const labelBBox = label.getBBox();
          // const icon = group.addShape('circle', {
          //   attrs: {
          //     x: labelBBox.maxX + 10,
          //     y: (labelBBox.minY + labelBBox.maxY) / 2,
          //     r: 5,
          //     stroke: '#000'
          //   },
          //   name: 'circle-shape',
          //   draggable: true
          // });
          const bboxWidth = label.getBBox().width + 20;
          rect.attr({ width: bboxWidth });
          group.addShape('path', {
            attrs: {
              lineWidth: 1,
              fill: '#ccc',
              stroke: '#0092ff',
              path: [['M', 0, 0], ['L', bboxWidth, 0]]
            },
            name: 'path-shape',
            draggable: true
          })
          return rect;
        }
      });
      //获取宽度
      const width = document.getElementById('mind').scrollWidth;
      const graph = new G6.TreeGraph({
          container: 'mind',
          width,
          height: vm.height,
          pixelRatio: 2,
          modes: {
            default: ['collapse-expand', 'drag-canvas', 'zoom-canvas']
        },
        // 节点类型及样式
        defaultNode: {
          type: 'rect',
          // size: 16,
          width:'auto',
          anchorPoints: [[0, 0.5], [1, 0.5]],
          style: {
            fill: '#005ff2',//背景色
            stroke: '#005ff2',//边框
          },
          labelCfg:{
            style:{
              fill: '#ffffff',
              fontSize
            }
          }
        },
        // 连线类型及样式
        defaultEdge: {
          type: 'cubic-horizontal',
          // polyline
          style: {
            stroke: '#0092ff'
          }
        },
        //布局
        layout: {
          type: 'mindmap',
          direction: 'H',
          getHeight: function getHeight() {
            return 16;
          },
          getWidth: function getWidth() {
            return 16;
          },
          getVGap: function getVGap() {
            return 10;
          },
          getHGap: function getHGap() {
            return 100;
          }
        }
      });
      graph.node(function (node) {
          // depth 类似节点标识
          if(node.depth == 0){
              return {
                  // size:[100,60],
                  style:{
                      fill: '#005ff2',//背景色
                      stroke: '#005ff2',//边框
                  },
                  // label:node.id
              }
          }
          if(node.depth == 1){
              return {
                  style:{
                      fill:'l(0) 0:rgba(0,36,186,1) 0.5:rgba(0,36,186,0.5) 1:rgba(0,0,0,0.1)',
                  },
              }
          }
           if(node.depth == 2){
              return {
                type:"line"
              }
          }
          return {
              // label: node.id, // 设置显示名称
              labelCfg: {
                  // position: node.children && node.children.length > 0 ? 'left' : node.x > centerX ? 'right' : 'left', // 设置显示左右
                  offset: 5
              }
          };
      });
      graph.data(this.data);
      graph.render();
      graph.fitView();
    },
  }
</script>
<style lang="scss" scoped>
  #mind{
    width: 100%;
    height: 100%;
  }
</style>