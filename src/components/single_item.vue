<template>
    <div v-if="item.state && (listType==='all'|| listType==='ok')" class="item">
        <span>{{item.name}}</span>
        <span class="ok itemState">&nbsp 已完成 &nbsp</span>
    </div>
    <div v-if="!item.state && (listType==='all'|| listType==='notOk')" class="item">
        <span style="text-decoration:line-through;">{{item.name}}</span>
        <span class="notOk itemState">&nbsp 未完成 &nbsp</span>
    </div>
</template>

<script>
    export default {
        name: "single_item",
        props: {
            item: {},
            listType: {type: String}
        },
    }
</script>

<style scoped>
    .itemState {
        border-radius: 15px;
    }

    .ok {
        background-color: #a4fa22;
    }

    .notOk {
        background-color: #ffbd40;

    }

    .item {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        margin-bottom: 8px;
    }

</style>
