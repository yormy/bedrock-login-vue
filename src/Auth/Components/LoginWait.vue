<template>
    <div>
        <y-title :title="$t('bedrock_login::auth.login_wait.title')"></y-title>

        <y-appearing-bullets
            :messages="messages"
        >

        </y-appearing-bullets>

    </div>
</template>

<script>
import YTitle from './../../Title.vue'
import {YAppearingBullets, YButtonPrimary} from 'bedrock-ui-vue'

/**
 *
 */
export default {
    inheritAttrs: false,

    components: {
        YAppearingBullets,
        YButtonPrimary,
        YTitle
    },

    data() {
        return {
            messages: [
                {
                    text: this.$t('bedrock_login::auth.login_wait.message.line1'),
                    loading: false,
                    completed: false,
                    processingMs: 1000,
                },
                {
                    text: this.$t('bedrock_login::auth.login_wait.message.line2'),
                    loading: false,
                    completed: false,
                    processingMs: 2000,
                },
                {
                    text: this.$t('bedrock_login::auth.login_wait.message.line3'),
                    loading: false,
                    completed: false,
                    processingMs: 2000,
                },
                {
                    text: this.$t('bedrock_login::auth.login_wait.message.line4'),
                    loading: false,
                    completed: false,
                    processingMs: 20000,
                },
            ],
        };
    },
}
</script>
