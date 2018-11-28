<template>
    <form ref="form" v-on:submit.prevent="onSubmit">
        <textarea id="list-code" name="list-code" ref="code" placeholder="Paste your Json code here..." autofocus></textarea>
        <a id="process-btn" class="btn" href="#" v-on:click.prevent="onSubmit">
            Process
        </a>
    </form>
</template>

<script>
export default {
    methods: {
        onSubmit() {
            if (this.$refs.code.value.length) {
                this.$emit('input', this.$refs.code.value);
            }
        }
    },
    mounted () {
        this.$refs.code.focus();
    }
}
</script>
