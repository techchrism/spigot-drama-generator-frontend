<template>
    <v-text-field readonly :value="value" :label="label">
        <template slot="append">
            <v-btn icon title="Copy to Clipboard" @click="copy" :color="copyColor">
                <v-icon>mdi-clipboard-arrow-right-outline</v-icon>
            </v-btn>
            <v-btn icon title="Share" v-if="canShare" @click="share">
                <v-icon>mdi-share-variant</v-icon>
            </v-btn>
        </template>
    </v-text-field>
</template>

<script>
    export default {
        name: 'TextShare',
        props: {
            value: String,
            label: String,
            description: String
        },
        data: () => ({
            copyColor: ''
        }),
        watch: {
            value()
            {
                this.copyColor = '';
            }
        },
        methods: {
            copy()
            {
                window.navigator.clipboard.writeText(this.description + ' - ' + this.value).then(() =>
                {
                    this.copyColor = 'success';
                });
            },
            share()
            {
                window.navigator.share({
                    url: this.value,
                    text: this.description
                });
            }
        },
        computed: {
            canShare()
            {
                return !!window.navigator.share;
            }
        }
    };
</script>

<style scoped>

</style>
