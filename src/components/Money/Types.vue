<template>
  <div>
    <ul class="types">
      <li :class="{[classPrefix+'-item']: classPrefix, selected: value==='-' }"
          @click="selectType('-')">支出
      </li>
      <li :class="{[classPrefix+'-item']: classPrefix, selected: value==='+ ' }"
          @click="selectType('+')">收入
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component, Prop, Watch} from 'vue-property-decorator';

@Component
export default class Types extends Vue {
  @Prop({default: '-'}) readonly value!: string;
  @Prop(String) classPrefix?: string;

  selectType(type: string) { // type is enum '-', ''
    if (type !== '-' && type !== '+') {
      throw new Error('Type is unkown!');
    }
    this.$emit('update:value', type);
  }
}
</script>

<style lang="scss" scoped>
.types {
  background: #c4c4c4;
  display: flex;
  text-align: center;
  font-size: 24px;

  > li {
    width: 50%;
    height: 64px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;

    &.selected::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 4px;
      background: #333;
    }
  }
}
</style>