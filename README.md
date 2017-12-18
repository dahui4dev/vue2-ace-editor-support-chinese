# vue2-ace-editor-support-chinese ![](https://img.shields.io/badge/vue-v2.0-green.svg) ![](https://img.shields.io/badge/license-GPL%20license-blue.svg)

A packaging of [ace](https://ace.c9.io/) support chinese, and support autocomplete.

基于ace、vue2的支持中文的组件包

支持自动补全功能

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
                // 这里需要哪种语言就引用那种，需要那个主题就用哪个。
                // Import which one you want.
                require('brace/mode/javascript');
                require('brace/theme/github');
            }
        },
    }
    ```
    
4. Use the component in template（以下是两种不同使用方法）

    * Direct use of v-model binding variables;（直接使用 v-model 绑定变量）
        ```
        <editor v-model="content" 
            @init="editorInit();"
            :autoComplete=true
            @setCompletions="setCompletions"
            lang="html" theme="chrome" width="500" height="100"></editor>
        ```
        
        prop `v-model`  is required（v-model必须）
        
        prop `lang` and `theme` is same as [ace-editor's doc](https://github.com/ajaxorg/ace)
        
        prop `height` and `width` could be one of these:  `200`, `200px`, `50%`
        
        prop `autoComplete` can define whether autoComplete is enabled（此标志定义自动提示，是否开启）
        
        prop `setCompletions` autoComplete callback（自动提示回调函数，在编辑器内容变化时触发，参数有四个） 
    
    * Separate value and input separately;（分别指定input 和 value）
        ```
        <editor @init="editorInit();" 
                @input="changeData"
                @setCompletions="setCompletions"
                :autoComplete=true 
                :value='editData'
                lang="html" theme="chrome" width="500" height="100"></editor>

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
              
                /**
                 * 设置自动补全回调函数，value变化实时执行。
                 * @param editor ace editor对象
                 * @param session
                 * @param pos 当前字符位置：row、column
                 * @param prefix 当前编辑字符
                 * @param callback 执行函数
                 */
                setCompletions (editor, session, pos, prefix, callback) {
                  let wordList = ['提示']
                  callback(null, wordList.map(function (word) {
                    return {
                      caption: word,
                      value: word,
                      meta: 'local'
                    }
                  }))
                }
            }
        }
        ```
        
        prop `@input` `:value` is required（必须）
        
        prop `lang` and `theme` is same as [ace-editor's doc](https://github.com/ajaxorg/ace)
        
        prop `height` and `width` could be one of these:  `200`, `200px`, `50%`
        
        prop `autoComplete` can define whether autoComplete is enabled（此标志定义自动提示，是否开启）
        
        prop `setCompletions` autoComplete callback（自动提示回调函数，在编辑器内容变化时触发，参数有四个） 

## License
[GPL许可证](http://www.gnu.org/licenses/gpl.html)