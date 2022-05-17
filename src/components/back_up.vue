<template>
    <div style="">
        <el-card>
            <template #header>
                <el-input v-model="task" placeholder="请输入要添加的待办事项">
                    <template #prepend>任务</template>
                    <template #append>
                        <el-button @click="addTask">添加</el-button>
                    </template>
                </el-input>
                <el-alert title="点击单个备忘就可以切换完成状态" type="success" style="margin-top: 10px" />
            </template>
            <div @click="changeState(o)" v-for="o in taskList">
                <single_item style="width: max-content;"
                             :listType="listType" :item="o"/>
            </div>

            <div style="text-align: center;">
                <el-button type="primary"
                           plain
                           id="zls-button-active"
                           @click="checkByDocAuthority('all')">
                    全部
                </el-button>
                <el-button type="primary"
                           plain
                           @click="checkByDocAuthority('ok')">
                    已完成
                </el-button>
                <el-button type="primary"
                           plain
                           @click="checkByDocAuthority('notOk')">
                    未完成
                </el-button>
            </div>
        </el-card>
    </div>
</template>

<script>
    import Single_item from "./single_item.vue";

    export default {
        name: "back_up",
        components: {Single_item}
    }
</script>
<script setup>
    import {ref} from 'vue';

    let taskList = ref([
        {name: "做晚饭", state: false},
        {name: "做早饭", state: true},
        {name: "做中饭", state: true},
        {name: "做明天的早饭", state: false},
        {name: "做明天的中饭", state: false},
        {name: "做明天的晚饭", state: false}
    ]);

    let task = ref("");

    function addTask() {
        taskList.value.push({name: task.value, state: false});
        task.value = "";
    }

    let listType = ref("all");

    function checkByDocAuthority(type) {
        //去除点击样式
        //如果有默认选中的按钮
        let buttons = document.getElementById("zls-button-active");
        //去除id
        if (buttons) {
            buttons.id = "";
        }
        listType.value = type;

        //获取当前触发该方法的dom元素
        let target = event.currentTarget;
        //添加按钮点击样式
        target.id = "zls-button-active";
    }

    function changeState(item) {
        console.dir(item);
        item.state = !item.state;
        console.dir(item);
    }
</script>

<style scoped>

</style>
