<template>
  <input
    type="checkbox"
    v-model="checked"
  />
</template>

<script lang="ts">
import { Component, Prop, Vue, Watch } from "vue-property-decorator";

@Component
export default class CheckboxComponent extends Vue {
  @Prop({ default: false }) value!: boolean;
  private checked = this.value;

  @Watch("checked")
  private clickCheckbox() {
    this.$emit("input", this.checked);
    console.log("checked",this.checked);
  }
}
</script>
