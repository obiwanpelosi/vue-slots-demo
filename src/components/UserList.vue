<script setup>
import { onMounted, ref } from "vue";

const userList = ref([]);
const loading = ref(true);

function remove(item) {
  userList.value = userList.value.filter(
    (user) => user.login.uuid !== item.login.uuid
  );
}

async function fetchUsers() {
  try {
    const response = await fetch("https://randomuser.me/api/?results=10");
    const data = await response.json();
    userList.value = data.results;
  } catch (error) {
    console.error("Error fetching data: ", error);
  } finally {
    loading.value = false;
  }
}
onMounted(() => {
  setTimeout(() => {
    fetchUsers();
  }, 2000);
});
</script>
<template>
  <div>
    <slot name="title" :count="userList.length">Users</slot>
    <slot
      name="userlist"
      :list="userList"
      :remove="remove"
      v-if="!loading && userList.length"
    >
      <ul class="userlist">
        <li v-for="item in userList" :key="item.email" class="list-item">
          <slot name="listitem" :user="item">
            <div>
              <img
                width="48"
                height="48"
                :src="item.picture.large"
                :alt="item.name.first + ' ' + item.name.last"
              />
              <div>
                <div>{{ item.name.first }}</div>
                <slot name="secondrow" :item="item"></slot>
              </div>
            </div>
          </slot>
        </li>
      </ul>
    </slot>
    <slot v-if="loading" name="loading">Loading...</slot>
  </div>
</template>

<style scoped>
ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 1em;
}
li.list-item > div {
  display: flex;
  gap: 1em;
}
li img {
  border-radius: 50%;
  width: 50px;
  height: 50px;
}
</style>
