<template>
    <div>
        <y-title :title="$t('bedrock_login::auth.reset_password.title')"></y-title>


            <div class="flex flex-col">
                <y-form-validated
                    :errors="form.messages.error"
                    :submit-label="$t('bedrock_login::auth.action.password_request_change')"
                    @submit="onResetPasswordHandler"
                >

                    <y-input-text
                        :hint-text="$t('bedrock_login::auth.field.email.hint')"
                        :label="$t('bedrock_login::auth.field.email.label')"
                        :label-help-description="$t('bedrock_login::auth.field.email.description')"
                        :placeholder="$t('bedrock_login::auth.field.email.placeholder')"
                        :rules="'required|email|min:5'"
                        field-name="email"
                    >
                    </y-input-text>

                    <y-input-text
                        :hint-text="$t('bedrock_login::auth.reset_password.field.password_new.hint')"
                        :is-password="true"
                        :label="$t('bedrock_login::auth.reset_password.field.password_new.label')"
                        :label-help-description="$t('bedrock_login::auth.reset_password.field.password_new.description')"
                        :placeholder="$t('bedrock_login::auth.reset_password.field.password_new.placeholder')"
                        :rules="'required'"
                        v-model="form.data.password"
                        field-name="password"
                    >
                    </y-input-text>

                    <y-input-text
                        :hint-text="$t('bedrock_login::auth.reset_password.field.password_confirm.hint')"
                        :is-password="true"
                        :label="$t('bedrock_login::auth.reset_password.field.password_confirm.label')"
                        :label-help-description="$t('bedrock_login::auth.reset_password.field.password_confirm.description')"
                        :placeholder="$t('bedrock_login::auth.reset_password.field.password_confirm.placeholder')"
                        :rules="'required|confirmed:@password'"
                        field-name="passwordConfirm"
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
import {
    YInputText,
    YCheckBox,
    YFormValidated
} from 'bedrock-ui-vue'

/**
 *
 */
export default {
    inheritAttrs: false,

    components: {
        YTitle,
        YInputText,
        YCheckBox,
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

        onResetPasswordHandler() {
        console.log('go resest');
        }
    }
}
</script>
