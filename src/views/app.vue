<template>
    <section id="main">
        <header>
            <h1>JSON CheckList Builder</h1>
        </header>
        <code-box v-on:input="onSubmit" />
        <div class="error" v-if="error">{{ error }}</div>
        <article id="tree">
            <ul class="node-tree">
                <node-tree v-for="(child, index) in nodes" v-bind:key="index" v-bind:value="child" v-bind:id="index" v-bind:isChecked="false" />
            </ul>
        </article>
        <selected-items />
    </section>
</template>

<script>
import codeBox from '../components/code-box.vue';
import nodeTree from '../components/node.vue';
import selectedItems from '../components/selected-items.vue';

export default {
    components: {
        codeBox,
        nodeTree,
        selectedItems
    },
    data () {
        return {
            nodes: null,
            error: null,
        }
    },
    methods: {
        onSubmit (code) {
            try {
                this.nodes = JSON.parse(code);
                this.error = null;
                console.log("Parsed Json:", this.code);
            } catch (e) {
                console.log("An error has ocurred while parsing your code");
                this.error = "An error has ocurred while parsing your code";
            }
        }
    }
}
</script>
<style>
#main {
    width: 80%;
    background-color: #f1f1f1;
    text-align: center;
    margin: auto;
}
#main h1 {
    color: #4d9900;
}

#list-code {
    margin: auto;
    width: 60%;
    height: 100px;
    display: block;
}

#main a.btn {
    background-color: #4caf50;
    border: none;
    color: white;
    margin: 5px;
    padding: 7px 15px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
}

#tree {
    display: flex;
}

#tree ul.node-tree, #tree ul.node-tree ul {
    list-style-type: none;
    margin: 5px;
}

#tree ul li {
    padding: 7px;
}

#main aside {
    display: flex;
}
</style>
