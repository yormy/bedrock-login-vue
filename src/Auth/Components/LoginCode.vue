<template>
    <div>
        <y-title
            :subtitle="$t('auth.login_code.subtitle')"
            :title="$t('auth.login_code.title')"
        ></y-title>

        <y-input-code
            :hint-text="$t('auth.login_code.hint')"
            :label="$t('auth.login_code.label')"
            fieldId="1"
            fieldName="code"
            @change="onCodeChange"
            @complete="onCodeComplete"
            @enter="onCodeEnter"
            v-on="$listeners"
        >
            <!--        :api-errors="args.apiErrors"-->
        </y-input-code>
        <y-button-primary :label="$t('auth.login_code.button')" class="mt-3"></y-button-primary>

    </div>
</template>

<script>
import YTitle from './../../Title.vue'
import {YInputCode, YButtonPrimary} from 'bedrock-ui-vue'

/**
 *
 */
export default {
    inheritAttrs: false,

    components: {
        YInputCode,
        YButtonPrimary,
        YTitle
    },

    data() {
        return {
            confirmCode: null,
            confirmCodeInvalid: null,
        }
    },

    methods: {
        onCodeChange() {
            this.confirmCode = null;
        },

        onCodeComplete(value) {
            this.confirmCodeInvalid = false;
            this.confirmCode = value;
        },

        onCodeEnter() {
            //this.loginAction();
        },
    }

}
</script>
