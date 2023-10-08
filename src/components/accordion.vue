<template>
  <v-expansion-panels>
    <v-expansion-panel :rounded="'lg'" @change="panelChange">
      <v-expansion-panel-title
        :expand-icon="ExandedIcon"
        :collapse-icon="ColapsedIcon"
      >
        <h1 contenteditable="true" ref="editableTitle">Заголовок</h1>
      </v-expansion-panel-title>
      <v-expansion-panel-text>
        <span contenteditable="true" ref="editableText">Текст</span>
      </v-expansion-panel-text>
    </v-expansion-panel>
  </v-expansion-panels>
</template>

<script setup lang="ts">
import { ref, onMounted, h } from "vue";
import Icon from "../assets/accordion-icon.svg";

const editableTitle = ref<HTMLElement | null>(null);
const editableText = ref<HTMLElement | null>(null);

const expandedStyle = {
  transform: "rotate(180deg)",
};

const ColapsedIcon = () => {
  return h("img", {
    src: Icon,
  });
};

const ExandedIcon = () => {
  return h("img", {
    src: Icon,
    style: expandedStyle,
  });
};

onMounted(() => {
  if (editableTitle.value && editableText.value) {
    editableTitle.value.textContent = "Заголовок";
    editableText.value.textContent = "Текст";
  }
});

const panelChange = (expanded: boolean) => {
  if (!expanded && editableTitle.value && editableText.value) {
    // При закрытии панели восстанавливаем содержимое текста
    editableTitle.value.textContent = "Заголовок";
    editableText.value.textContent = "Текст";
  }
};
</script>

<style lang="scss">
.accordion-card {
  padding: 30px;
}
</style>
