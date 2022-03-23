<template>
  <li>
    <h2>{{ name }} {{ isFavorite ? "(Favorite)" : "" }}</h2>

    <button @click="toggleFavorite">Toggle Favorite</button>
    <button @click="toggleDetails">
      {{ detailsAreVisible ? "Hide" : "Show" }} Details
    </button>

    <ul v-if="detailsAreVisible">
      <li><strong>Phone: </strong>{{ phoneNumber }}</li>
      <li><strong>Email: </strong>{{ emailAddress }}</li>
    </ul>
    <button @click="$emit('delete', id)">Delete</button>
  </li>
</template>

<script>
export default {
  // props: ["name", "phoneNumber", "emailAddress", "isFavorite"],

  props: {
    id: {
      type: String,
      required: true,
    },
    name: { type: String, equired: true },
    phoneNumber: { type: String, required: true },
    emailAddress: { type: String, required: true },
    isFavorite: {
      type: Boolean,
      default: false,
      // validator: function (value) {
      //   return value === "1" || value === "0";
      // },
    },
  },

  emits: ["toggle-favorite", "delete"],
  // emits: {
  //   "toggle-favorite": function (id) {
  //     if (id) {
  //       return true;
  //     } else {
  //       console.warn("ID is Missing!!");
  //       return false;
  //     }
  //   },
  // },

  data() {
    return {
      detailsAreVisible: false,
    };
  },

  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFavorite() {
      // this.friendIsFavorites = !this.friendIsFavorites;
      this.$emit("toggle-favorite", this.id);
    },
    // deleteFriend(){
    //   this.$emit('delete');
    // },
  },
};
</script>