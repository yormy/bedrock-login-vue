<template>
    <ValidationObserver ref="validationObserver" v-slot="{ invalid, handleSubmit }">
        <form @submit.prevent="handleSubmit(onSubmitHandler)">

            <slot></slot>

            <y-alert-text-danger :message="errors"></y-alert-text-danger>

            <div class="mt-3">
                <y-button-primary :is-disabled="invalid" :label="submitLabel"></y-button-primary>
            </div>

        </form>

    </ValidationObserver>


</template>

<script>

import {
    YButtonPrimary,
    YAlertTextDanger
} from 'bedrock-ui-vue'

/**
 *
 */
export default {
    inheritAttrs: false,

    components: {
        YButtonPrimary,
        YAlertTextDanger
    },

    props: {
        errors : {},

        submitLabel : {
            type: String,
            required : true
        }
    },

    data() {
        return {
        }
    },

    methods: {
        onSubmitHandler() {
            this.$emit('submit');
        },
    },
}
</script>
