<template>
    <li class="node">
        <input type="checkbox" ref="checkbox" v-model="shouldBeChecked" v-bind:id="'label-' + id" name="label" v-on:change="toggleCheck($event)" />

        <label v-bind:for="'label-' + id">{{ value.name }}</label>

        <ul v-if="children && children.length">
            <node v-for="(child, index) in children" v-bind:key="index" v-bind:value="child" v-bind:id="id + '-' + index" v-bind:isChecked="checked" v-on:check="check" v-on:uncheck="uncheck" />
        </ul>
    </li>
</template>

<script>
export default {
    name: 'node',
    props: {
        id: {
            required: false
        },
        value: {
            required: false
        },
        isChecked: {
            type: Boolean
        }
    },
    data () {
        return {
            checked: this.isChecked,
            children: this.value.children ? this.value.children.slice() : [],
            checkedChildren: [],
        }
    },
    computed: {
        allChildrenUnchecked () {
            return this.children && (this.checkedChildren.length == 0);
        },
        shouldBeChecked: {
            get () {
                return this.checked || this.isChecked;
            },
            set (value) {
                this.checked = value;
            }
        }
    },
    methods: {
        check (node) {
            if (-1 < this.children.indexOf(node) && this.checkedChildren.indexOf(node) == -1) {
                console.log('pushed');
                this.checkedChildren.push(node);
            }
            console.log(this.children);
            console.log("Check", node);

            var r = this.children.indexOf(node);
            console.log("Found:", r);
            console.log(this.value.name, this.checkedChildren.length);

            this.checked = true;
            this.$emit('check', this.value);
        },
        uncheck (node) {
            if (-1 < this.checkedChildren.indexOf(node)) {
                console.log('popped');
                this.checkedChildren.pop();
            }

            console.log("Uncheck", node);
            console.log(this.children);
            console.log(this.value.name, this.checkedChildren.length);


            if (this.allChildrenUnchecked) {
                this.checked = false;
                this.$emit('uncheck', this.value);
            }
        },
        toggleCheck (event) {
            this.$emit(event.target.checked ? 'check' : 'uncheck', this.value);
        }
    }
}
</script>
