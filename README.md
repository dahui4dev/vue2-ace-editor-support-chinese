# vue2-ace-editor-support-chinese ![](https://img.shields.io/badge/vue-v2.0-green.svg) ![](https://img.shields.io/badge/license-GPL%20license-blue.svg)

A packaging of [ace](https://ace.c9.io/) support chinese

基于ace、vue2的支持中文的组件包

## How to use（如何使用）

1. Install

    ```
    npm install --save-dev vue2-ace-editor-support-chinese
    ```
    
2. Require it in `components` of Vue options（推荐使用 ES6 写法）

    ```
    import editor from "vue2-ace-editor-support-chinese";

    export default {
        data(){
              return {}
        },
        methods,
        ...
        components: { editor },
    }
    ```
 
3. Require the editor's mode/theme module in custom methods
    
    ```
    {
        data,
        methods:{
            editorInit:function () {
                require('vue2-ace-editor-support-chinese/node_modules/brace/mode/html');
                require('vue2-ace-editor-support-chinese/node_modules/brace/mode/javascript');
                require('vue2-ace-editor-support-chinese/node_modules/brace/mode/groovy');
                require('vue2-ace-editor-support-chinese/node_modules/brace/theme/chrome');
            }
        },
    }
    ```
    
4. Use the component in template（以下是两种不同方法使用）

    * Direct use of v-model binding variables;（直接使用 v-model 绑定变量）
        ```
        <editor v-model="content" @init="editorInit();" lang="html" theme="chrome" width="500" height="100"></editor>
        ```
        
        prop `v-model`  is required（v-model必须）
        
        prop `lang` and `theme` is same as [ace-editor's doc](https://github.com/ajaxorg/ace)
        
        prop `height` and `width` could be one of these:  `200`, `200px`, `50%`
    
    * Separate value and input separately;（分别指定input 和 value）
        ```
        <editor @init="editorInit();" lang="html" theme="chrome" width="500" height="100"
                @input="changeData" :value='editData'></editor>

        {
            data(){
              return {
                editData: editData //初始展示数据，必要时三目运算判空
              }
            },
            methods: {
              // value变化触发input执行，
              changeData: function (context) {
                this.editData = context;
              },
            }
        }
        ```
        
        prop `@input` `:value` is required（必须）
        
        prop `lang` and `theme` is same as [ace-editor's doc](https://github.com/ajaxorg/ace)
        
        prop `height` and `width` could be one of these:  `200`, `200px`, `50%`

## License
[GPL许可证](http://www.gnu.org/licenses/gpl.html)