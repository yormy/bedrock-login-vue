<template>
    <div>
        <y-title
            :subtitle="$t('bedrock_login::auth.login_email_code.subtitle')"
            :title="$t('bedrock_login::auth.login_email_code.title')"
        ></y-title>

        <y-input-code
            :hint-text="$t('bedrock_login::auth.login_email_code.hint')"
            :label="$t('bedrock_login::auth.login_email_code.label')"
            fieldId="1"
            fieldName="code"
            v-on="$listeners"
            :error-text="apiMessage"
        >
        </y-input-code>

        <div class="">
            <y-check-box
                v-if="allowTrustIp"
                v-model="trustIp"
                :label="$t('bedrock_login::auth.login.field.whitelist_ip.label')"
                :modal-description="$t('bedrock_login::auth.login.field.whitelist_ip.description')"
                field-id="3"
                field-name="whitelist_ip"
                styling="text-small is-greyed"
                @input="$emit('update:trustIp', $event)"
            >
            </y-check-box>
            <y-check-box
                v-if="allowTrustBrowser"
                v-model="trustBrowser"
                :label="$t('bedrock_login::auth.login.field.whitelist_browser.label')"
                :modal-description="$t('bedrock_login::auth.login.field.whitelist_browser.description')"
                field-id="4"
                field-name="whitelist_browser"
                styling="text-small is-greyed"
                @input="$emit('update:trustBrowser', $event)"
            >
            </y-check-box>
        </div>

        <div class="mt-3">

        </div>

        <div class="flex justify-between">
            <y-button-primary :label="$t('bedrock_login::auth.action.verify')" @click="$emit('verify')">
            </y-button-primary>
            <a class="text-small is-greyed" @click="$emit('back')">{{
                    $t('bedrock_login::auth.action.login')
                }}</a>
        </div>

    </div>
</template>

<script>
import YTitle from './../../Title.vue'
import {YInputCode, YButtonPrimary, YCheckBox} from 'bedrock-ui-vue'

/**
 *
 */
export default {
    inheritAttrs: false,

    components: {
        YInputCode,
        YButtonPrimary,
        YTitle,
        YCheckBox
    },

    props: {
        /**
         * Show a checkbox to allow the user to indicate that theit IP needs to be whitelisted
         */
        allowTrustIp: {
            type: Boolean,
            default: false,
        },

        /**
         * Show a checkbox to allow the user to indicate that theit Browser needs to be whitelisted
         */
        allowTrustBrowser: {
            type: Boolean,
            default: false,
        },

        apiMessage: {
            type: String,
            default: '',
        },
    },

    data() {
        return {
            confirmCode: null,
            confirmCodeInvalid: null,

            trustIp: false,
            trustBrowser: false,
        }
    },

}
</script>
