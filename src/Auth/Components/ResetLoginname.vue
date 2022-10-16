<template>
    <div>
        <y-title :title="$t('bedrock_login::auth.reset_loginname.title')"></y-title>

        <div class="flex flex-col">
            <y-form-validated
                :errors="form.messages.error"
                :submit-label="$t('bedrock_login::auth.action.loginname_request_change')"
                @submit="onResetLoginnameHandler"
            >
                <y-input-text
                    :hint-text="$t('bedrock_login::auth.field.email.hint')"
                    :label="$t('bedrock_login::auth.field.email.label')"
                    :label-help-description="$t('bedrock_login::auth.field.email.description')"
                    :placeholder="$t('bedrock_login::auth.field.email.placeholder')"
                    :rules="'required|email|min:5'"
                    fieldId="1"
                    fieldName="email"
                >
                </y-input-text>

                <y-input-text
                    :hint-text="$t('bedrock_login::auth.reset_loginname.field.loginname_new.hint')"
                    :label="$t('bedrock_login::auth.reset_loginname.field.loginname_new.label')"
                    :label-help-description="$t('bedrock_login::auth.reset_loginname.field.loginname_new.description')"
                    :placeholder="$t('bedrock_login::auth.reset_loginname.field.loginname_new.placeholder')"
                    :rules="'required|min:5'"
                    fieldId="1"
                    fieldName="new loginname"
                >
                </y-input-text>
            </y-form-validated>

            <div class="mt-3 text-right">
                <a class="is-greyed" @click="onReturnLoginHandler">{{
                        $t('bedrock_login::auth.navigation.to_login')
                    }}</a>
            </div>

        </div>
    </div>
</template>

<script>
import YTitle from './../../Title.vue'
import {YInputText, YCheckBox, YButtonPrimary, YFormValidated} from 'bedrock-ui-vue'

/**
 *
 */
export default {
    inheritAttrs: false,

    components: {
        YTitle,
        YInputText,
        YCheckBox,
        YButtonPrimary,
        YFormValidated
    },

    data() {
        return {
            form: {
                data: {
                    password : 'aa',
                },

                messages: {},
                apiErrors: {},
            },
        }
    },

    methods: {
        onReturnLoginHandler() {
            this.$emit('onReturnToLoginClicked');
        },

        onResetLoginnameHandler() {

        }

    }
}
</script>
