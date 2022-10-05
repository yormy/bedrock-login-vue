<template>
    <div>
        <y-title :title="$t('auth.reset_selector.title')"></y-title>

        <div class="mt-3">
            <y-button-primary :label="$t('auth.label.password')" class="mt-3"
                              @click="onResetPasswordHandler"></y-button-primary>
            <y-button-primary :label="$t('auth.label.loginname')" class="mt-3"
                              @click="onResetLoginnameHandler"></y-button-primary>
        </div>
        <div class="mt-3 text-right">
            <a class="is-greyed" @click="onReturnLoginHandler">{{
                    $t('auth.navigation.to_login')
                }}</a>
        </div>
    </div>
</template>


<script>
import YTitle from './../../Title.vue'
import {YButtonPrimary} from 'bedrock-ui-vue'

/**
 *
 */
export default {
    components: {
        YTitle,
        YButtonPrimary,
    },

    methods: {
        onResetPasswordHandler() {
            this.$emit('onResetPasswordClicked');
        },
        onResetLoginnameHandler() {
            this.$emit('onResetLoginnameClicked');
        },
        onReturnLoginHandler() {
            this.$emit('onReturnToLoginClicked');
        }
    }
}
</script>
