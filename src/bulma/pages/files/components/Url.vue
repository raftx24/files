<template>
    <modal v-on="$listeners"
        :show="show">
        <div class="box">
            <div class="field has-addons">
                <div class="control is-expanded">
                    <input class="input"
                        :value="link"
                        v-select-on-focus
                        v-focus>
                </div>
                <div class="control">
                    <a class="button"
                        @click="copy">
                        <span class="icon is-small">
                            <fa icon="copy"/>
                        </span>
                    </a>
                </div>
            </div>
        </div>
    </modal>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core';
import { faCopy } from '@fortawesome/free-solid-svg-icons';
import { focus, selectOnFocus } from '@enso-ui/directives';
import { Modal } from '@enso-ui/modal/bulma';

library.add(faCopy);

export default {
    name: 'Url',

    directives: { focus, selectOnFocus },

    components: { Modal },

    inject: ['i18n'],

    props: {
        show: {
            type: Boolean,
            required: true,
        },
        link: {
            type: String,
            default: '',
            required: true,
        },
    },

    methods: {
        copy() {
            document.execCommand('copy');
            this.$toastr.success(this.i18n('Copied to clipboard'));
        },
    },
};
</script>
