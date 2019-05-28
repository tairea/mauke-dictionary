<template>
    <div id="app">
        <h1 class="title">연락처</h1>
        <div class="list-wrap">
            <AlphabetList :list="list" />
        </div>
    </div>
</template>

<script>
import contact from './contact.json'
import AlphabetList from './components/AlphabetList'

export default {
    name: 'App',
    components: {
        AlphabetList
    },
    data () {
        return {
            list: contact.data
        }
    }
}
</script>

<style lang="scss">
@import url("~reset-css/reset.css");

html, body {
    width: 100%;
    height: 100%;
}

#app {
    width: 100%;
    height: 100%;
    padding: 40px 10px;
    box-sizing: border-box;

    .title {
        font-size: 2em;
        font-weight: bold;
        margin-bottom: 10px;
    }

    .list-wrap {
        position: relative;
    }
}
</style>