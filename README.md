## vue-paginate
A awesome paginate component for vue.js(2.x)

 ![image](https://github.com/falstack/vue-paginate/raw/master/demo.png)

## 项目依赖：
vue.js(2.x)

vue-resource(1.x)

lodash

**PS：需配合后台才能显示数据**

**后台接口参数格式：**

方式：GET

字段：

    limit:10
    
    offset:0
    
    sortby:id
    
    order:desc
    
    id(可为空): (any)
    
如：laravel.dev/get/datas?limit=10&offset=0&sortby=id&order=desc

## api
#### 引入：
````javascript
// .html
components: {
    'paginate': window.vuePaginate
},

// .vue
import paginate from '../paginate.vue'
components : {
    paginate
},
````
#### 使用：
````html
<paginate :template="template" :init="init"></paginate>
````
#### 初始化：
````javascript
template : 必须，html模板，如：
"<div class='item'>" +
    "<p>{{ item.title }}</p>" +
"</div>"
````
**PS：{{ item.title }}中，item用于v-for，不能修改。其中title字段是数据字段，根据你自己的数据来自定义**
````javascript
init：必须，object，如：
{
  // 定义后台数据接口地址，必须 | required | string
  api: 'xxxx',
  // 定义后台返回数据的格式，用于vue-resource读取 | required | Object
  // data：列表数据key，必须。例中的data读取格式为response.body.data
  // total：后台数据总数，必须。李忠total读取格式为response.body.meta.total
  res: {
      data: 'data',
      total: 'meta.total'
  },
  // 用于排列数据的字段，以及在<select>中显示的文字，如果为空，则不显示<select>
  sorts: [
      {val: "id", name: "最新发布"}, {val: "like", name: "最多喜欢"}, {val: "talk", name: "最多回复"}
  ],
  // 用于定义数据是降序还是升序，可为空。default : 'desc' | string in ['desc', 'asc']
  order: 'desc',
  // 用于初始化数据时的排序字段，可为空。default：'id' | string
  sortby: 'id',
  // 用于定义每次获取的数据数量，可为空。default：10 | number && >0
  limit : 10，
  // 定义获取数据的id字段，如/user/1的文章或/user/2的文章，可为空。 default : undefined
  id : undefined
}
````

## demo
````html
<!--html-->
<head>
    <link rel="stylesheet" href="./dist/vue-paginate.css">
</head>
<body>
    <div id="warp">
        <paginate :template="template" :init="init"></paginate>
    </div>
</body>
//javascript
<script src="http://cdn.bootcss.com/vue/2.0.1/vue.min.js"></script>
<script src="http://cdn.bootcss.com/vue-resource/1.0.3/vue-resource.min.js"></script>
<script src="http://cdn.bootcss.com/lodash.js/4.16.2/lodash.min.js"></script>
<script src="./bulid/vue-paginate.js"></script>
<script>
    new Vue({
        el: '#warp',
        components: {
            'paginate': window.vuePaginate
        },
        data () {
            return {
                template:
                "<div class='item'>" +
                    "<p>{{ item.title }}</p>" +
                "</div>",
                init: {
                    api: 'http://localhost:8000/api/article/all',
                    res: {
                        data: 'data',
                        total: 'meta.total'
                    },
                    sorts: [
                        {val: "id", name: "最新发布"}, {val: "like", name: "最多喜欢"}, {val: "talk", name: "最多回复"}
                    ]
                }
            }
        }
    })
</script>
````
