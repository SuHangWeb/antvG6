# antv G6 图表-思维导图 在vue中使用

### 调用方法（单独页面调用）

> import 引用
```
 import mind from './modules/mind.vue'
```

> 注册组件
```
components {
    mind
}
```

### 组件使用
```
<mind :data="dataJson" :height="mindHeight"/>
```
* dataJson 数据
* height 动态高度 （一般设置 当前图表组件的父元素的高度就好 最好动态获取）

#### dataJson 数据格式示例

```
{
    "id": "id1",
    "label": "遗属补助小专项",
    "children": [{
            "id": "id1-1",
            "label": "已死亡",
            "children": [{
                    "id": "id1-1-1",
                    "label": "问题数：35个"
                },
                {
                    "id": "id1-1-2",
                    "label": "人数：50人"
                },
                {
                    "id": "id1-1-3",
                    "label": "资金：340万"
                }
            ]
        },
        {
            "id": "id1-2",
            "label": "姓名与身份证不符",
            "children": [{
                    "id": "id1-2-1",
                    "label": "问题数：35个"
                },
                {
                    "id": "id1-2-2",
                    "label": "人数：50人"
                },
                {
                    "id": "id1-2-3",
                    "label": "资金：340万"
                }
            ]
        },
        {
            "id": "id1-3",
            "label": "未查到身份证信息",
            "children": [{
                    "id": "id1-3-1",
                    "label": "问题数：35个"
                },
                {
                    "id": "id1-3-2",
                    "label": "人数：50人"
                },
                {
                    "id": "id1-3-3",
                    "label": "资金：340万"
                }
            ]
        },
        {
            "id": "id1-4",
            "label": "领取低保",
            "children": [{
                    "id": "id1-4-1",
                    "label": "问题数：35个"
                },
                {
                    "id": "id1-4-2",
                    "label": "人数：50人"
                },
                {
                    "id": "id1-4-3",
                    "label": "资金：340万"
                }
            ]
        },
        {
            "id": "id1-5",
            "label": "年龄不符合",
            "children": [{
                    "id": "id1-5-1",
                    "label": "问题数：35个"
                },
                {
                    "id": "id1-5-2",
                    "label": "人数：50人"
                },
                {
                    "id": "id1-5-3",
                    "label": "资金：340万"
                }
            ]
        }
    ]
}
```