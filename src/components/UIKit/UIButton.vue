
<template>
    <button class="ui-btn" @click="onClickBtn"
        :class="{
            'ui-btn-xsmall': xsmall,
            'ui-btn-small': small,
            'ui-btn-large': large,
            'ui-btn-xlarge': xlarge,
            'ui-btn-tile': tile,
            'ui-btn-rounded': rounded,
            'ui-btn-circle': circle,
            'ui-btn-disabled': disabled,
        }"
        :style="`
            --color-tint: ${TintColor};
        `"
    >
        <slot>Button</slot>
    </button>
</template>


<script lang="ts">
import { Component, Vue, Emit, Prop } from 'vue-property-decorator';
// 米修在线
// QQ 群: 2122-7101
@Component
export default class UIButton extends Vue {

    @Prop(Boolean) private xsmall: boolean | undefined;
    @Prop(Boolean) private small: boolean | undefined;
    @Prop(Boolean) private large: boolean | undefined;
    @Prop(Boolean) private xlarge: boolean | undefined;
    @Prop(Boolean) private tile: boolean | undefined;
    @Prop(Boolean) private rounded: boolean | undefined;
    @Prop(Boolean) private circle: boolean | undefined;
    @Prop(Boolean) private disabled: boolean | undefined;
    @Prop(String) private color: string | undefined;

    @Emit('click') private emitClickEvent(event: MouseEvent) {}

    private get TintColor() {
        if (this.color) {
            return this.color;
        } else {
            return '#2D8CF0';
        }
    }

    private onClickBtn(event: MouseEvent) {
        if (!this.disabled) {
            this.emitClickEvent(event);
        }
    }
}
</script>


<style lang="stylus" scoped>
resize(minWidth, height, paddingLR, fontSize)
    min-width minWidth
    height height
    padding 0 paddingLR
    font-size fontSize
    &.ui-btn-rounded, &.ui-btn-circle
        border-radius (@height / 2)
    &.ui-btn-circle
        width @height
        min-width 0
        padding 0

.ui-btn
    resize(64px, 36px, 16px, 0.875rem)
    border 0 solid black
    border-radius 4px
    color #17233D
    background-color var(--color-tint)
    font-weight 500
    letter-spacing 0.09em
    cursor pointer
    user-select none 
    outline none 
    transition filter 0.2s linear
    &:hover
        filter brightness(120%)
    &:active
        filter brightness(80%)
    &.ui-btn-xsmall
        resize(36px, 20px, 9px, 0.625rem)
    &.ui-btn-small
        resize(50px, 28px, 12px, 0.75rem)
    &.ui-btn-large
        resize(78px, 44px, 19px, 0.875rem)
    &.ui-btn-xlarge
        resize(92px, 52px, 23px, 1rem)
    &.ui-btn-tile
        border-radius 0
    &.ui-btn-disabled
        background-color #F5F5F5
        color #C5C8CE
        cursor not-allowed
</style>
