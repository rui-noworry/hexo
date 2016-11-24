---
title: vuex配置流程
date: 2016-11-24 10:33:32
tags: vue
categories: vue
---


使用vuex 1.0配置流程

（1）在mutation-types里定义一个函数变量名，意义：函数名出错
export const SHOW_DIALOG = "SHOW_DIALOG"; // 显示弹窗

（2）在actions声明这个函数
// 显示弹窗
// 注意两个以上的参数 用对象的方式
    showDialog({dispatch}, { state, msg}) {
        dispatch(types.SHOW_DIALOG, { state, msg})
    }

（3）在store/modules中创建一个confirm.js文件编写初始状态并写mutations逻辑

import {
    SHOW_DIALOG
} from '../mutation-types';

const Confirm = {
    initialState: {
        msg: '请填写完整信息',
        state: false
    },
    mutations: {
        /**
         * 设置显示状态并传入信息
         * @param state是否显示dialog
         * @param  msg 显示的信息
         */
         [SHOW_DIALOG]({confirm}, {state, msg}) { // 这里的{confirm}是index里声明的
            if (msg)
                confirm.msg = msg;

            confirm.state = state;
        }
    }
}

export default Confirm;

（4）在index.js里声明
``` bash
	import Vue from 'vue'
import Vuex from 'vuex'
import actions from './actions'
import Core from './modules/core'
import Auth from './modules/auth'
import Course from './modules/course'
import EnterpriseAuth from "./modules/enterpriseAuth";
**import Confirm from './modules/confirm';**

Vue.use(Vuex);

const debug = process.env.NODE_ENV !== 'production';

export default new Vuex.Store({
    state: {
        core: Core.initialState,
        auth: Auth.initialState,
        course: Course.initialState,
        enterpriseAuth : EnterpriseAuth.initialState,
       ** confirm: Confirm.initialState**
    },
    actions,
    mutations: [].concat(
        Core.mutations,
        Auth.mutations,
        Course.mutations,
        EnterpriseAuth.mutations,
        **Confirm.mutations**
    ),
    strict: false,
    middlewares: debug ? [ Vuex.createLogger() ] : []
})

```

(5)在组件中调用

``` bash
<template>
    <article class="confirm-container" v-show="state">
        <section class="confirm-wrap">
            <div class="confirm-content">
                <p>{{msg}}</p>
                <a href="javascript:;" @click="closeConfirm()">确定</a>
            </div>
        </section>
    </article>
</template>
<style lang="scss">
    @import "../../components/common/_mixins.scss";
        .confirm-container{
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.4);
            position:fixed;
            top:0;
            left: 0;
            right: 0;
            bottom: 0;
            z-index:999;

            .confirm-wrap{
                margin: 0 auto;
                margin-top: 50%;
                width: 80%;
                max-width: 412px;
                height: px2rem(400);
                background: #fff;
                position: relative;
                box-shadow:1px 1px 5px #000;
                border-radius:px2rem(30);

                p{
                    text-align: center;
                    height: px2rem(236);
                    line-height: px2rem(236);
                    font-size: px2rem(54);
                    color: #555;
                }
                a{
                    display: block;
                    width: 100%;
                    height: px2rem(158);
                    border-top:1px solid #ededed;
                    font-size: px2rem(54);
                    color: #17bda9;
                    line-height: px2rem(158);
                    text-align: center;
                    position: absolute;
                    bottom: 0;

                }
            }
            @media (min-width: 999px) {
                .confirm-wrap{
                    height:195px;
                    border-radius:15px;
                    margin-top:20%;
                    p{
                        height:114px;
                        line-height:114px;
                        font-size: 26px;
                    }
                    a{
                        height:78px;
                        line-height:78px;
                        font-size:26px;
                    }
                }
            }
        }
</style>
<script class="babel">
    import store from '../../store/index';
    import actions from "../../store/actions";

    export default{
        vuex: {
            actions // 注意要注册action
        },
        computed:{ // 用于监听属性的状态, 对于状态实时改变的，就要用computed关键字
            state(){ // 方法名就是属性名
                return store.state.confirm.state;
            },
            msg(){
                return store.state.confirm.msg
            }
        },
        data(){
            return {
                msg:store.state.confirm.msg
            }
        },
        methods:{
            closeConfirm(){
                actions.showDialog(store,{state:false,msg:''});
            }
        }
    }
</script>
```
