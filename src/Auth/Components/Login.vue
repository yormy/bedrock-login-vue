<template>
<div>
    <y-title :title="$t('auth.login.title')"></y-title>

    {{ form.data }}
    <y-login-wait v-if="isLoginWait">
    </y-login-wait>

    <input v-model="form.data.firstname" name="'firstname'" type="hidden"/>

    <y-login-email-code
        v-if="isEmailCode"
        :allow-trust-browser="allowTrustBrowser"
        :allow-trust-ip="allowTrustIp"
        :api-message="state.emailCodeError"
        :hint="$t('auth.login_email_code.hint')"
        :label="$t('auth.login_email_code.label')"
        :subtitle="$t('auth.login_email_code.subtitle')"
        :title="$t('auth.login_email_code.title')"
        :trust-browser.sync="form.data.trust_browser"
        :trust-ip.sync="form.data.trust_ip"
        @back="onToLogin"
        @change="onCodeChange"
        @complete="onCodeComplete"
        @enter="onCodeEnter"
        @verify="onLoginHandler"
    >
    </y-login-email-code>

    <div v-if="!state.screen" class="flex flex-col">
        <ValidationObserver ref="validationObserver" v-slot="{ handleSubmit }">
            <form @submit.prevent="handleSubmit(onLoginHandler)">
                <y-input-text
                    v-model="form.data.loginname"
                    :api-errors="form.apiErrors"
                    :hint-text="$t('auth.field.loginname.hint')"
                    :label="$t('auth.field.loginname.label')"
                    :label-help-description="$t('auth.field.loginname.description')"
                    :placeholder="$t('auth.field.loginname.placeholder')"
                    :rules="'required|min:5'"
                    field-id="loginname"
                    field-name="loginname"
                >
                </y-input-text>

                <y-input-text
                    v-model="form.data.password"
                    :api-errors="form.apiErrors"
                    :hint-text="$t('auth.field.password.hint')"
                    :is-password="true"
                    :label="$t('auth.field.password.label')"
                    :label-help-description="$t('auth.field.password.description')"
                    :placeholder="$t('auth.field.password.placeholder')"
                    :rules="'required|strong-password'"
                    fieldId="password"
                    fieldName="password"
                >
                </y-input-text>

                <div class="flex justify-between">
                    <y-check-box
                        v-model="form.data.remember"
                        :description="$t('auth.login.field.remember_me.description')"
                        :label="$t('auth.login.field.remember_me.label')"
                        field-id="3"
                        field-name="remember"
                        styling="text-small is-greyed"
                    >
                    </y-check-box>
                    <a class="text-small is-greyed" @click="onForgotHandler">{{
                            $t('auth.action.forgot')
                        }}</a>
                </div>

                <y-alert-text-danger :message="form.messages.error"></y-alert-text-danger>

                <div class="mt-3">
                    <y-button-primary :label="$t('auth.action.login')"></y-button-primary>
                </div>

            </form>

        </ValidationObserver>

    </div>
  </div>
</template>

<script>
import YTitle from './../../Title.vue'

import {
    YInputText,
    YCheckBox,
    YButtonPrimary,
    YAlertTextDanger

} from 'bedrock-ui-vue'
import YLoginWait from './LoginWait.vue'
import YLoginEmailCode from './LoginEmailCode.vue'

const SCREEN = {
    LOGINWAIT: 'LOGINWAIT',
    EMAILCODE: 'EMAILCODE'
}
/**
 *
 */
export default {
    inheritAttrs: false,

    components: {
        YInputText,
        YCheckBox,
        YButtonPrimary,
        YTitle,
        YAlertTextDanger,
        YLoginWait,
        YLoginEmailCode
    },

    props: {
        asAdmin: {
            type: Boolean,
            default: false,
        },

        /**
         * Show a checkbox to allow the user to indicate that theit IP needs to be whitelisted
         */
        allowTrustIp: {
            type: Boolean,
            default: true,
        },

        /**
         * Show a checkbox to allow the user to indicate that theit Browser needs to be whitelisted
         */
        allowTrustBrowser: {
            type: Boolean,
            default: true,
        },

    },

    data() {
        return {
            dummy: '',
            form: {
                data: {
                    loginname: 'joe@bounty.com',
                    password: 'Welkom1!',
                    firstname: '',          //honeypot
                    remember: false,
                    emailCode: '',
                    authenticatorCode: null,
                    trust_ip: false,
                    trust_browser: false,
                },

                messages: {},
                apiErrors: {},


            },

            routesMember: {
                login: 'member.account.login.store'
            },
            routesAdmin: {
                login: 'admin.account.login.store'
            },

            state: {
                screen: null,
                formDataValid: false,
                emailCodeError: null,
            }
        }
    },

    computed: {
        isLoginWait() {
            return this.state.screen === SCREEN.LOGINWAIT;
        },
        isEmailCode() {
            return this.state.screen === SCREEN.EMAILCODE;
        },
    },

    mounted() {
        this.clearErrors();
    },

    methods: {
        onToLogin() {
            this.state.screen = null;
            this.clearCodeFormData();
            this.form.messages = {};
        },

        onCodeChange() {
            this.form.data.emailCode = null;
        },

        onCodeComplete(value) {
            this.form.data.emailCode = value;
        },

        onCodeEnter(value) {
            this.form.data.emailCode = value;
            this.onLoginHandler();
        },

        onForgotHandler() {
            this.$emit('onForgotClicked');
        },

        getRoute() {
            let route = '';
            route = this.routesMember.login;

            if (this.asAdmin) {
                route = this.routesAdmin.login;
            }

            return this.route(route);
        },

        // validateForm() {
        //     // const provider = this.$refs.yinput.$refs.validationrefname;
        //     // provider.validate();
        //     this.$refs.validationObserver.validate();
        //
        //     return this.$refs.validationObserver.flags.valid;
        // },


        onLoginHandler() {
            this.state.screen = SCREEN.LOGINWAIT;
            this.clearErrors();
            const that = this;
            this.$http
                .post(this.getRoute(), this.form.data)
                .then((success) => {
                    this.form.data = {};
                    this.form.messages.success = success.data.message;
                    const permissions = success.data.data.permissions;
                    // storePermissions(permissions, this.asAdmin);

                    const redirectTo = success.data.redirect_to;
                    window.setTimeout(() => {
                        window.location.href = redirectTo;
                    }, 0);

                    // reset screen to login, so on browser back the login screen is visible again,
                    // not loading screen
                    window.setTimeout(() => {
                        this.state.screen = null;
                    }, 20000);

                })
                .catch((error) => {
                    this.form.apiErrors = error.response.data.data;
                    this.form.messages.error = error.response.data.message;

                    if (error.response.data.code) {
                        if (error.response.data.code === 'LOGIN_EMAIL_CODE_MISSING') {
                            this.clearCodeFormData();
                            this.state.screen = SCREEN.EMAILCODE;
                            return;
                        }
                    }

                    if (error.response.data.code) {
                        if (error.response.data.code === 'LOGIN_EMAIL_CODE_INVALID') {
                            this.clearCodeFormData();
                            this.state.screen = SCREEN.EMAILCODE;
                            this.state.emailCodeError = error.response.data.message;
                            return;
                        }
                    }
                    this.state.screen = null;
                })
                .finally(() => {
                });
        },

        clearCodeFormData() {
            this.form.data.emailCode = '';
            this.form.data.authenticatorCode = null;
            this.form.data.trust_ip = false;
            this.form.data.trust_browser = false;
        },

        clearErrors() {
            this.form.messages = {
                error: '',
                success: '',
                warning: '',
            }

            this.form.apiErrors = null;
        }
    }
}
</script>