<script setup lang="ts">
import { ref } from "vue";
const notifications = ref([
  {
    name: "Mark Webber",
    event: "Reaction",
    post: "My first tournament today",
    created_at: "1 min ago",
    avatar: "./images/avatar-mark-webber.webp",
    read: false,
  },
  {
    name: "Angela Gray",
    event: "follow",
    created_at: "5 min ago",
    avatar: "./images/avatar-angela-gray.webp",
    read: false,
  },
  {
    name: "Jacob Thompson",
    event: "Joined club",
    group: "Chess Club",
    created_at: "1 day ago",
    avatar: "./images/avatar-jacob-thompson.webp",
    read: false,
  },
  {
    name: "Rizky Hasanuddin",
    event: "sent message",
    group: "Chess Club",
    created_at: "5 day ago",
    avatar: "./images/avatar-rizky-hasanuddin.webp",
    message:
      "Hello, thanks for setting up the Chess Club. I've been a member for a few weeks now and I'm already having lots of fun and improving my game. ",
    read: true,
  },
  {
    name: "Kimberly Smith",
    event: "comment",
    picture: "./images/image-chess.webp",
    created_at: "1 week ago",
    avatar: "./images/avatar-kimberly-smith.webp",
    read: true,
  },
  {
    name: "Nathan Peterson",
    event: "Reaction",
    post: "5 end-game strategies to increase your win rate",
    created_at: "2 weeks ago",
    avatar: "./images/avatar-nathan-peterson.webp",
    read: true,
  },
  {
    name: "Anna Kim",
    event: "Left club",
    group: "Chess Club",
    created_at: "2 weeks ago",
    avatar: "./images/avatar-anna-kim.webp",
    read: true,
  },
]);
const unRead = ref(0);
const markRead = () => {
  notifications.value = notifications.value.map((notification) => {
    return {
      ...notification,
      read: true,
    };
  });

  unRead.value = 0;
};
notifications.value.forEach((notification) => {
  return notification.read === false ? unRead.value++ : unRead.value;
});
</script>

<template>
  <header>
    <h1>
      Notifications <span v-if="unRead > 0">{{ unRead }}</span>
    </h1>
    <button @click="markRead">Mark all as read</button>
  </header>
  <ul>
    <li v-for="notification in notifications" :key="notification.name">
      <img :src="notification.avatar" :alt="notification.avatar" />
      <div v-if="notification.event === 'Reaction'">
        <p>
          {{ notification.name }} reacted
          <span class="notice">{{ notification.post }}</span>
          <span class="red"></span>
        </p>
        <p>{{ notification.created_at }}</p>
      </div>
      <div v-if="notification.event === 'follow'">
        <p>{{ notification.name }} followed you <span class="red"></span></p>
        <p>{{ notification.created_at }}</p>
      </div>
      <div v-if="notification.event === 'Joined club'">
        <p>
          {{ notification.name }} has joined your group
          <span class="notice">{{ notification.group }}</span>
          <span class="red"></span>
        </p>
        <p>{{ notification.created_at }}</p>
      </div>
      <div v-if="notification.event === 'comment'">
        {{ notification.name }} commented on your picture
        <span>{{ notification.created_at }}</span>
        <img :src="notification.picture" />
      </div>
      <div v-if="notification.event === 'Left club'">
        <div>
          <p>
            {{ notification.name }} left the group
            <span>{{ notification.group }}</span>
          </p>
          <p>{{ notification.created_at }}</p>
        </div>
      </div>
      <div v-if="notification.event === 'sent message'">
        <div>
          <p>{{ notification.name }} sent you a private message</p>
          <p>{{ notification.created_at }}</p>
        </div>

        <p class="message">{{ notification.message }}</p>
      </div>
    </li>
  </ul>
</template>
