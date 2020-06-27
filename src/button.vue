<template>
  <button class="g-button" :class="{[`icon-${iconPosition}`]: true}">
    <g-icon class="icon" v-if="icon" :name="icon"></g-icon>
    <g-icon class="loading" v-if="icon" name="loading"></g-icon>
    <div class="content">
      <slot></slot>
    </div>
  </button>
</template>

<script>
  export default {
    props: {
      icon: {},
      iconPosition: {
        type: String,
        default: 'left',
        validator(value) {
          return value === 'left' || value === 'right';
        }
      }
    }
  }
</script>

<style lang="scss">
  @keyframes spin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }

  .g-button {
    display: inline-flex;
    justify-content: center;
    align-items: center;
    vertical-align: middle;
    line-height: 14px;
    font-size: var(--font-size);
    height: var(--button-height);
    padding: 0 1em;
    border-radius: var(--border-radius);
    border: 1px solid var(--border-color);
    background: var(--button-bg);

    > .content {
      order: 2;
    }

    > .icon {
      order: 1;
      vertical-align: middle;
      margin-right: .1em;
    }

    &:hover {
      border-color: var(--border-color-hover);
    }

    &:active {
      background: var(--button-active-bg);
    }

    &:focus {
      outline: none;
    }

    &.icon-right {
      > .content {
        order: 1;
      }

      > .icon {
        margin-left: .1em;
        margin-right: 0;
        order: 2;
      }

    }
    .loading {
      animation: spin 2s infinite linear;
    }
  }
</style>