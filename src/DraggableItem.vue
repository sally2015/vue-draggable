<template>
    <div class="draggable-item">
        <slot></slot>
    </div>
</template>
<script>
export default {
    name: 'DraggableItem',
    props: ['index', 'item'],
    data: function () {
        return {
            collection: 'default'
        }
    },
    inject: ['manager'],
    watch: {
        index(newIndex) {
            if (this.$el) {
                this.$el.sortableInfo.newIndex = newIndex;
            }
        },
        item: {
            handler(newItem) {
                if (this.$el) {
                    this.$el.sortableInfo.item = newItem;
                }
            },
            deep: true
        }
    },
    mounted() {
        this.collection = this.getClosetDraggable(this)._uid;
        this.initItem(this.index, this.item);
    },
    beforeDestroy() {
        this.removeDraggable();
    },
    methods: {
        initItem(index, item) {
            const node = this.$el;
            node.sortableInfo = {
                index,
                item
            }
            this.ref = node;
            this.manager.add(this.ref, this.collection);
        },
        removeDraggable() {
            this.manager.remove(this.ref, this.collection);
        },
        getClosetDraggable(com) {
            let parentCom = com.$parent;
            if (!parentCom) {
                return null;
            } else if (parentCom.$options.name === 'Draggable') {
                return parentCom
            } else {
                return this.getClosetDraggable(parentCom);
            }
        }
    }
}
</script>


