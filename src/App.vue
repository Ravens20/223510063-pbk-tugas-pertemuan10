<template>
  <div>
    <nav>
      <ul>
        <li :class="{ active: selectedMenu === 'registration' }" @click="selectedMenu = 'registration'">Todos</li>
        <li :class="{ active: selectedMenu === 'posts' }" @click="selectedMenu = 'posts'">Posts</li>
      </ul>
    </nav>
    <div>
      <RegistrationForm 
        v-if="selectedMenu === 'registration'"
        @activity-added="handleActivityAdded"
        @activity-cancelled="handleActivityCancelled"
      />
      <UserPosts 
        v-if="selectedMenu === 'posts'"
        :users="users"
        @user-selected="handleUserSelected"
        @posts-fetched="handlePostsFetched"
      />
    </div>
  </div>
</template>

<script>
import RegistrationForm from './components/RegistrationForm.vue';
import UserPosts from './components/UserPosts.vue';

export default {
  components: {
    RegistrationForm,
    UserPosts,
  },
  data() {
    return {
      selectedMenu: 'registration',
      users: [],
      posts: [],
    };
  },
  methods: {
    handleActivityAdded(activity) {
      console.log('Activity added:', activity);
    },
    handleActivityCancelled(activity) {
      console.log('Activity cancelled:', activity);
    },
    handleUserSelected(userId) {
      console.log('User selected:', userId);
    },
    handlePostsFetched(posts) {
      console.log('Posts fetched:', posts);
      this.posts = posts;
    },
  },
};
</script>

<style scoped>
nav {
  background-color: #fff;
  padding: 10px;
  border-bottom: 2px solid #eee;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
  display: flex;
  justify-content: center;
}

li {
  margin: 0 20px;
  padding: 10px 20px;
  cursor: pointer;
  font-weight: bold;
  color: #555;
  transition: color 0.3s, background-color 0.3s;
}

li:hover {
  color: #007bff;
}

.active {
  color: #fff;
  background-color: #007bff;
  border-radius: 4px;
}
</style>
