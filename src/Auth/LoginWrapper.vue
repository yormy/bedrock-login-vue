<template>
    <div>
        <login
            v-if="showCredentials"
            @onForgotClicked="onForgotClicked"
        >
        </login>

        <reset-selector
            v-if="showResetSelector"
            @onResetLoginnameClicked="onResetLoginnameClicked"
            @onResetPasswordClicked="onResetPasswordClicked"
            @onReturnToLoginClicked="onReturnToLoginClicked"
        ></reset-selector>

        <reset-password
            v-if="showResetPassword"
            @onReturnToLoginClicked="onReturnToLoginClicked"
        ></reset-password>

        <reset-loginname
            v-if="showResetLoginname"
            @onReturnToLoginClicked="onReturnToLoginClicked"
        ></reset-loginname>

    </div>
</template>

<script>
import Login from './Components/Login.vue'
import ResetSelector from './Components/ResetSelector.vue'
import ResetPassword from "./Components/ResetPassword.vue";
import ResetLoginname from "./Components/ResetLoginname.vue";

const SCREEN = {
    CREDENTIALS: 'CREDENTIALS',
    RESET_SELECTOR: 'RESET_SELECTOR',
    RESET_PASSWORD: 'RESET_PASSWORD',
    RESET_LOGINNAME: 'RESET_LOGINNAME',
};

/**
 *
 */
export default {
    inheritAttrs: false,

    components: {
        Login,
        ResetSelector,
        ResetLoginname,
        ResetPassword,
    },


    data() {
        return {
            show: null,
        }
    },

    computed: {
        showCredentials() {
            return this.show === null || this.show === SCREEN.CREDENTIALS;
        },
        showResetSelector() {
            return this.show === SCREEN.RESET_SELECTOR;
        },
        showResetPassword() {
            return this.show === SCREEN.RESET_PASSWORD;
        },
        showResetLoginname() {
            return this.show === SCREEN.RESET_LOGINNAME;
        }
    },

    methods: {
        onForgotClicked() {
            this.show = SCREEN.RESET_SELECTOR;
        },

        onResetPasswordClicked() {
            this.show = SCREEN.RESET_PASSWORD;
        },

        onResetLoginnameClicked() {
            this.show = SCREEN.RESET_LOGINNAME;
        },

        onReturnToLoginClicked() {
            this.show = SCREEN.CREDENTIALS;
        }

    }
}
</script>
