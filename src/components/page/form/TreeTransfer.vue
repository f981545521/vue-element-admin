<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item>
                    <i class="el-icon-lx-calendar"></i> 表单
                </el-breadcrumb-item>
                <el-breadcrumb-item>TreeTransfer表单</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="container">
            <div class="form-box">
                <tree-transfer :title="title" :from_data='fromData' :to_data='toData' :defaultProps="{label:'label'}"
                               @addBtn='add' @removeBtn='remove' :mode='mode' height='540px' filter openAll>
                </tree-transfer>
            </div>
        </div>
    </div>
</template>

<script>
    /**
     * 树形穿梭：参考：https://github.com/hql7/tree-transfer
     *          演示：https://hql7.github.io/lib/dist/index.html
     */
    import treeTransfer from 'el-tree-transfer';

    export default {
        name: 'treeTransferForm',
        data() {
            return {
                title: ["源列表", "目标列表"],
                mode: "transfer", // transfer addressList
                fromData: [
                    {
                        id: "1",
                        pid: 0,
                        label: "一级 1",
                        children: [
                            {
                                id: "1-1",
                                pid: "1",
                                label: "二级 1-1",
                                disabled: true,
                                children: []
                            },
                            {
                                id: "1-2",
                                pid: "1",
                                label: "二级 1-2",
                                children: [
                                    {
                                        id: "1-2-1",
                                        pid: "1-2",
                                        children: [],
                                        label: "二级 1-2-1"
                                    },
                                    {
                                        id: "1-2-2",
                                        pid: "1-2",
                                        children: [],
                                        label: "二级 1-2-2"
                                    }
                                ]
                            }
                        ]
                    },
                ],
                toData: [
                    {
                        id: "2-1",
                        pid: "1",
                        label: "你好",
                        children: []
                    }
                ]
            }
        },
        methods: {
            // 切换模式 现有树形穿梭框模式transfer 和通讯录模式addressList
            changeMode() {
                if (this.mode == "transfer") {
                    this.mode = "addressList";
                } else {
                    this.mode = "transfer";
                }
            },
            // 监听穿梭框组件添加
            add(fromData, toData, obj) {
                // 树形穿梭框模式transfer时，返回参数为左侧树移动后数据、右侧树移动后数据、移动的{keys,nodes,halfKeys,halfNodes}对象
                // 通讯录模式addressList时，返回参数为右侧收件人列表、右侧抄送人列表、右侧密送人列表
                console.log("fromData:", fromData);
                console.log("toData:", toData);
                console.log("obj:", obj);
            },
            // 监听穿梭框组件移除
            remove(fromData, toData, obj) {
                // 树形穿梭框模式transfer时，返回参数为左侧树移动后数据、右侧树移动后数据、移动的{keys,nodes,halfKeys,halfNodes}对象
                // 通讯录模式addressList时，返回参数为右侧收件人列表、右侧抄送人列表、右侧密送人列表
                console.log("fromData:", fromData);
                console.log("toData:", toData);
                console.log("obj:", obj);
            }
        },
        components: {treeTransfer} // 注册

    };
</script>