<template>
  <div>
    <b-form-group class="label-title text-left" label="Rule" label-for="rule-filter">
      <multiselect
        v-model="selectedRules"
        :options="options"
        :multiple="true"
        :show-labels="true"
        :close-on-select="true"
        :clear-on-select="false"
        :searchable="true"
        :preserve-search="true"
        :select-label="'Select'"
        :deselect-label="'Remove'"
        placeholder="Select Rule"
        :preselect-first="false"
        @input="onRuleFilterChange"
      >
        <span slot="noResult">No rule found</span>
      </multiselect>
    </b-form-group>
  </div>
</template>
<script>
import Multiselect from 'vue-multiselect';

export default {
  name: 'RuleFilter',
  props: {
    options: {
      type: Array,
      required: true,
    },
    requestedRuleFilterValue: {
      type: Array,
      required: false,
      default: () => [],
    },
  },
  data() {
    return {
      selectedRules: this.requestedRuleFilterValue,
    };
  },
  methods: {
    onRuleFilterChange() {
      if (this.selectedRules.length > 0) {
        this.$emit('on-rule-change', this.selectedRules);
      } else {
        this.$emit('on-rule-change', null);
      }
    },
    resetRuleFilterSelection() {
      this.selectedRules = this.requestedRuleFilterValue;
    },
  },
  watch: {
    requestedRuleFilterValue(newValue) {
      this.selectedRules = newValue;
    },
  },
  components: {
    Multiselect,
  },
};
</script>
<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>
