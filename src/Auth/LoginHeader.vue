<template>
    <div class="">
        <div class="flex justify-between">
            <div class="text-muted text-small">
                <div v-if="allowSignup">
                    Not a member ?
                    <a>Signup now</a>
                </div>
            </div>

            <!-- Language dropdown-->
            <div class="y-dropdown--container">
                <div v-if="allowLanguageSwitcher">
                    <!-- Dropdown toggle -->
                    <input id="checkbox-125" class="hidden y-dropdown--checkbox--input"
                           type="checkbox">
                    <label class="flex justify-end" for="checkbox-125">
                        <div class="y-dropdown--label">
                            <span class="flag-icon flag-icon-de"></span>
                        </div>
                        <div class="icon icon-dropdown"></div>
                    </label>

                    <!-- Dropdown card -->
                    <div class="y-dropdown--card right-aligned">
                        <a class="y-dropdown--item" href="#"> <span
                            class="flag-icon flag-icon-nl"></span> Dutch </a>
                        <a class="y-dropdown--item" href="#"> <span
                            class="flag-icon flag-icon-us"></span> English </a>
                    </div>
                </div>
            </div>
        </div>

        <div class="header flex-row ">
            <!--                <div class="brand&#45;&#45;name">Bedrock</div>-->
            <img class="brand--logo"
                 src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/24/LEGO_logo.svg/500px-LEGO_logo.svg.png">
        </div>

    </div>

</template>


<script>

/**
 * Show the header of the right page content
 * with logo and/or signup and language switcher
 */
export default {
    components: {},

    props: {

        /**
         * Show the signup link
         */
        allowSignup: {
            type: Boolean,
            default: true,
        },

        /**
         * Show the language switcher section
         */
        allowLanguageSwitcher: {
            type: Boolean,
            default: true,
        },
    }
}
</script>
