<template>
    <div class="alphabet-list">
        <ul class="list-nav">
            <li class="nav-item" v-for="(shortcut, index) in shortcuts" :key="index"><a :href="`#${shortcut}`">{{ shortcut }}</a></li>
        </ul>
        <div class="list-container">
            <AlphabetListItem v-for="(value, key, index) in groups" :key="index" :groupName="key" :items="value" />
        </div>
    </div>
</template>

<script>
import AlphabetListItem from './AlphabetListItem'

export default {
    name: 'AlphabetList',
    components: {
        AlphabetListItem
    },
    props: {
        list: {
            type: Array,
            default () {
                return []
            }
        }
    },
    data () {
        return {
            shortcuts: [],
            groups: {}
        }
    },
    methods: {
        groupByList (list = this.list, key = '') {
            const reducer = (result, value) => {
                const hash = (value[key] || '').charAt(0).toUpperCase()

                if (result.hasOwnProperty(hash)) {
                    result[hash].push(value)
                } else {
                    result[hash] = [value]
                }

                return result
            }

            return list.reduce(reducer, {})
        }
    },
    created () {
        this.groups = this.groupByList(undefined, 'title')
        this.shortcuts = Object.keys(this.groups)
    }
}
</script>

<style lang="scss" scoped>
.alphabet-list {
    position: relative;
    width: 100%;
    height: 100%;
}

.list-nav {
    position: absolute;
    top: 0;
    right: 0;
    width: 20px;
    height: 100%;
    text-align: center;

    .nav-item {
        cursor: pointer;
        
        a {
            color: inherit;
            text-decoration: none;
        }
    }
}
</style>