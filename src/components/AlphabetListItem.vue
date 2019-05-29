<template>
    <div class="alphabet-list-item">
        <p class="list-divider">{{ groupName }}</p>
        <ul class="list-item">
            <li class="item" v-for="(item, index) in sortedItems" :key="index">{{ item.title }}</li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'AlphabetListItem',
    props: {
        groupName: {
            type: String,
            default: ''
        },
        items: {
            type: Array,
            default () {
                return []
            }
        }
    },
    computed: {
        sortedItems () {
            const toUpperCase = (key) => (obj) => ( obj[key].toUpperCase() )
            const titleUpperCase = toUpperCase('title')
            const sort = (v1, v2) => ( titleUpperCase(v1) === titleUpperCase(v2) ? 0 : titleUpperCase(v1) > titleUpperCase(v2) ? 1 : -1 )

            return this.items.sort(sort)
        }
    }
}
</script>

<style lang="scss" scoped>
.list-divider {
    font-size: 0.8em;
    font-weight: bold;
    background: #e5e5e5;
    padding: 5px;
}

.item {
    font-size: 1.1em;
    padding: 10px;
    background: white;
    border-bottom: 1px solid #c3c3c3;
    box-sizing: border-box;

    &:last-child {
        border-color: transparent;
    }
}
</style>