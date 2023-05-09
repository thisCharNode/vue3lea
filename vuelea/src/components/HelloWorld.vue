<template>
<el-select v-model="select"  filterable placeholder="Select"
           :filter-method="filterTreeDate" >
    <el-option style="height: auto;width: auto" value="select">
        <el-tree
                :data="data"
                :props="defProps"
                ref="treeRef"
                node-key="treeKey"
                :filter-node-method="filterNode"
                @node-click =handleNodeClick
        />
<!--        @check="handleCheckChange"-->
    </el-option>
</el-select>
</template>
<script setup lang="ts">
import {ref, reactive, Ref} from 'vue'
const count = ref(0)
let select = ref('')
let data = reactive([
    {
        id: 1,
        label: 'Level one 1',
        children: [
            {
                id: 4,
                label: 'Level two 1-1',
                children: [
                    {
                        id: 9,
                        label: 'Level three 1-1-1',
                    },
                    {
                        id: 10,
                        label: 'Level three 1-1-2',
                    },
                ],
            },
        ],
    },
    {
        id: 2,
        label: 'Level one 2',
        children: [
            {
                id: 5,
                label: 'Level two 2-1',
            },
            {
                id: 6,
                label: 'Level two 2-2',
            },
        ],
    },
    {
        id: 3,
        label: 'Level one 3',
        children: [
            {
                id: 7,
                label: 'Level two 3-1',
            },
            {
                id: 8,
                label: 'Level two 3-2',
            },
        ],
    },
])
let option  = ref('')
let defProps = reactive({
    children: 'children',
    label: 'label',
})
let treeRef:Ref = ref(null)
defineProps({
    msg:{
        type:String,
    }
})
function filterNode (value,data){
    if (!value) return true
    return data.label.includes(value)
}
function filterTreeDate (val){
    // select.value = val
    treeRef.value.filter(val)
}
// function handleCheckChange(data,checked){
//     select.value = data.label
//     if (checked.checkedKeys !== '') {
//         treeRef.value.setCheckedKeys([data.id], true)
//     } else {
//         treeRef.value.setCheckedKeys([])
//     }
// }
function handleNodeClick(node: any) {
    select.value = node['label']
    select.value = node['label']
}
</script>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
