<template>
    <div>
        {{index}}-{{item.id}}
        <button @click="add('left', index)">左边添加</button>
      <button @click="add('right', index)">右边添加</button>
    </div>
</template>
<script>
export default {
    name: 'TableColumn1',
    props: {
        index: {
            type: Number,
            default: 0,
            require: true
        },
        item: {
            type: Object,
            default: () => {},
            require: true,
        }
    },
    watch: {
        item: {
            handler(newVal, oldVal) {
                // eslint-disable-next-line no-console
                console.log('newVal',newVal,oldVal);
            },
            immediate: true,
            deep: true
        }
    }, 
    methods: {
        add(type, index) {
            this.$emit('add', type, index);
        }
    }
}
</script>