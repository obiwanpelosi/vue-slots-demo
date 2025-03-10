<script setup>
import { ref } from "vue";
import UserList from "./components/UserList.vue";
import ListTitle from "./components/ListTitle.vue";
import CardList from "./components/CardList.vue";

const selected = ref("first");

const options = [
  { value: "first", label: "First Name" },
  { value: "last", label: "Last Name" },
  { value: "full", label: "Full name" },
  { value: "fullWithTitle", label: "Name with title" },
];
</script>

<template>
  <select v-model="selected">
    <option
      v-for="(option, index) in options"
      :key="index"
      :value="option.value"
    >
      {{ option.label }}
    </option>
  </select>
  <UserList>
    <template #title="{ count }">
      <ListTitle :count="count" />
    </template>
    <template #userlist="{ list, remove }">
      <CardList :list="list">
        <template #[selected]="{ text }">
          <h2>{{ text }}</h2>
        </template>
        <template #secondrow="{ item }">
          <button @click="remove(item)">Remove User</button>
        </template>
      </CardList>
    </template>
  </UserList>
</template>
