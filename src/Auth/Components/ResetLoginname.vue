<template>
    <div>
        <y-title :title="$t('bedrock_login::auth.reset_loginname.title')"></y-title>

        <div class="flex flex-col">
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

            <y-button-primary
                :label="$t('bedrock_login::auth.action.loginname_request_change')"
                class="mt-3"
            >
            </y-button-primary>

            <div class="mt-3 text-right">
                <a class="is-greyed" @click="onReturnLoginHandler">{{
                        $t('bedrock_login::auth.navigation.to_login')
                    }}</a>
            </div>

        </div>
    </div>
</template>
<!--v-model="modelValue"-->


<!--:error-text="args.errorText"-->
<!--:hide-label="args.hideLabel"-->
<!--:hint-text="args.hintText"-->
<!--:is-password="args.isPassword"-->
<!--:label-help-description="args.description"-->
<!--:label-help-text="'forgot password ?'"-->
<!--:label="args.label"-->
<!--:valid-text="args.validText"-->
<!--:api-errors="args.apiErrors"-->
<!--@onAppendClicked="onAppendClicked"-->
<!--@onEnter="onEnter"-->
<!--@onEsc="onEsc"-->
<!--@onKeyUp="onKeyUp"-->
<!--prefix-clicked="clicked"-->
<!--prefix="<i class='icon icon-warning'></i>"-->

<!--v-model="modelValue"-->


<script>
import YTitle from './../../Title.vue'
import {YInputText, YCheckBox, YButtonPrimary} from 'bedrock-ui-vue'

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
    },

    methods: {
        onReturnLoginHandler() {
            this.$emit('onReturnToLoginClicked');
        }
    }
}
</script>
