<template>
  <a :target="target" :href="link" class="button">
    <span class="button__icon-wrapper">
      <svg
        viewBox="0 0 14 15"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
        class="button__icon-svg"
        width="10"
      >
        <path
          d="M13.376 11.552l-.264-10.44-10.44-.24.024 2.28 6.96-.048L.2 12.56l1.488 1.488 9.432-9.432-.048 6.912 2.304.024z"
          fill="currentColor"
        ></path>
      </svg>

      <svg
        viewBox="0 0 14 15"
        fill="none"
        width="10"
        xmlns="http://www.w3.org/2000/svg"
        class="button__icon-svg button__icon-svg__copy"
      >
        <path
          d="M13.376 11.552l-.264-10.44-10.44-.24.024 2.28 6.96-.048L.2 12.56l1.488 1.488 9.432-9.432-.048 6.912 2.304.024z"
          fill="currentColor"
        ></path>
      </svg>
    </span>
    {{ name }}
  </a>
</template>

<script setup>
const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  link: {
    type: String,
    default: "#",
  },
  target: {
    type: String,
    default: "_self",
  },
});
</script>

<style lang="scss">
.button {
  line-height: 1;
  text-decoration: none;
  display: inline-flex;
  border: none;
  cursor: pointer;
  align-items: center;
  gap: 8px;
  background: var(--primary);
  color: var(--secondary);
  border-radius: 10rem;
  font-family: var(--alternate-font);
  padding: 4px 12px 4px 4px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  transition: background-color 0.3s;

  &__icon-wrapper {
    flex-shrink: 0;
    width: 32px;
    height: 32px;
    position: relative;
    color: var(--text);
    background: var(--bg);
    border-radius: 50%;
    display: grid;
    place-items: center;
    overflow: hidden;
  }

  &__icon-svg {
    &__copy {
      position: absolute;
      transform: translate(-150%, 150%);
    }
  }

  &:hover {
    background: var(--accent);
    color: var(--secondary);

    .button__icon-wrapper {
      background: var(--secondary);
      color: var(--accent);
    }

    .button__icon-svg {
      &:first-child {
        transition: transform 0.3s ease-in-out;
        transform: translate(150%, -150%);
      }

      &__copy {
        transition: transform 0.3s ease-in-out 0.1s;
        transform: translate(0);
      }
    }
  }
}
</style>