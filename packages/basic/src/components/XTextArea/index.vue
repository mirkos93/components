<template>
  <div>
    <inputLabel :label="label" :required="required" :description="description"/>
    <v-textarea
      v-bind="Object.assign({}, newProps, $attrs)"
      v-on="$listeners"
      :rules="innerRules"
    ></v-textarea>
  </div>
</template>

<script>
export default {
  name: 'x-textarea',
  props: {
    label: { type: String, default: '' },
    description: { type: String, default: '' },
    required: { type: Boolean, default: false },
    name: { type: String, default: '' },
    value: { type: String, default: '' },
    placeholder: { type: String, default: '' },
    appendIcon: { type: String, default: '' },
    prependIcon: { type: String, default: '' },
    errorMessages: { type: String, default: '' },
    disabled: { type: Boolean, default: false },
    rules: {}, //Array or Function, so no assigned here
    id: { type: String, default: undefined }
  },
  computed: {
    newProps() {
      const newProps = { ...this.$props };
      delete newProps.label;
      return newProps;
    }
  },
  data: function() {
    return {
      innerRules:
        this.rules ||
        (this.required
          ? [(v) => !!v || `${this.label || 'field'} is required`]
          : [])
    };
  }
};
</script>

<style lang="stylus" scoped>
@import '../../styles/_variables.styl';

.v-textarea {
  margin-top: 0;
  padding-top: 0;

  >>>.v-input__prepend-outer { /* prepend-icon */
    margin: 0;

    .v-input__icon {
      width: 50px;
      height: 50px;

      i {
        font-size: 25px;
        color: $slate-grey;

        &.primary--text {
          color: $secondary-01 !important;
        }
      }
    }
  }

  >>>.v-input__control {
    .v-input__slot {
      background: white;
      border: 1px solid $silver-two;
      border-radius: 3px;
      margin-bottom: 2px;

      &:before {
        display: none;
      }

      &:after {
        border-color: $secondary-01;
      }

      .v-text-field__slot {
        .v-text-field__prefix {
          width: auto;
          height: 48px;
          line-height: 48px;
          padding: 0 14px;
          background: rgba(183, 190, 200, 0.3);
          color: $slate-grey;
        }

        label {
          font-size: 14px;
          color: $slate-grey;
          font-weight: 600;
          top: -12px;
          left: 0 !important;

          .star {
            color: $primary-01;
          }
        }

        textarea {
          padding: 20px;
          color: $secondary-01;
          width: 100%;
          font-size: 16px;
          line-height: 1.5;
        }

        ::-webkit-input-placeholder { /* WebKit browsers */
          color: $silver-two;
        }

        ::-moz-placeholder { /* Mozilla Firefox 19+ */
          color: $silver-two;
        }

        :-ms-input-placeholder { /* Internet Explorer 10+ */
          color: $silver-two;
        }
      }

      .v-input__append-inner { /* text field icon */
        margin: 0;
        padding: 0;

        .v-input__icon {
          width: 48px;
          height: 48px;

          i {
            color: $silver;
            font-size: 20px;
          }
        }
      }
    }

    .v-text-field__details {
      .v-messages {
        height: 20px;
        font-size: 14px;
        &.error--text {
          color: $error !important;
          caret-color: $error !important;
        }
      }
    }
  }
}

.v-input--is-disabled { /* disable */
  >>> .v-input__control {
    .v-input__slot {
      background: $pale-grey-two !important;
    }
  }
}
</style>
