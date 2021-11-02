<template>
  <div>
    <div v-if="!person" class="profile__empty">Место пустое</div>
    <div v-else class="person">
      <div class="person__photo">
        <img :src="person.picture" alt="photo" />
      </div>
      <div class="person__info">
        <div class="person__info-name">
          <b>{{ person.name }} ({{ person.age }})</b>
        </div>

        <div class="person__info-email">Почта: {{ person.email }}</div>
        <div class="person__info-email">
          Дата регистрации: {{ formatedDate }}
        </div>
        <div class="person__info-about">О себе: {{ person.about }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import { format } from "date-fns";

export default {
  props: {
    person: {
      type: Object,
      default: null,
    },
    closeProfile: {
      type: Function,
    },
  },
  computed: {
    formatedDate() {
      return format(new Date(this.person.registered), "dd/MM/yyyy");
    },
  },
  mounted() {
    window.addEventListener("click", this.handleClick);
  },
  destroyed() {
    window.removeEventListener("click", this.handleClick);
  },
  methods: {
    handleClick(e) {
      if (!e.target.classList.contains("wrapper-table")) {
        this.closeProfile();
      }
    },
  },
};
</script>

<style scoped>
.person {
  display: grid;
  grid-template-columns: 50px 1fr;
  grid-gap: 8px;
}

.person__photo img {
  height: 50px;
  width: 50px;
  border-radius: 50%;
}

.person__info {
  display: grid;
  grid-gap: 8px;
}

.person__info-name {
  margin-bottom: 10px;
}
</style>
