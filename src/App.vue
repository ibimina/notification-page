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
    <div class="heading">
      <h1>Notifications</h1>
      <span v-if="unRead > 0" class="unread">{{ unRead }}</span>
    </div>
    <button @click="markRead">Mark all as read</button>
  </header>
  <ul>
    <li
      v-for="notification in notifications"
      :key="notification.name"
      :class="{ pale: !notification.read }"
    >
      <img
        :src="notification.avatar"
        :alt="notification.avatar"
        class="avatar"
      />
      <div v-if="notification.event === 'Reaction'">
        <p>
          <span class="name">{{ notification.name }}</span>
          <span class="action">reacted to your recent post</span>
          <span class="notice">{{ notification.post }}</span>
          <span :class="{ red: !notification.read }"></span>
        </p>
        <p class="time">{{ notification.created_at }}</p>
      </div>
      <div v-if="notification.event === 'follow'">
        <p>
          <span class="name">{{ notification.name }}</span>
          <span class="action">followed you</span>
          <span :class="{ red: !notification.read }"></span>
        </p>
        <p class="time">{{ notification.created_at }}</p>
      </div>
      <div v-if="notification.event === 'Joined club'">
        <p>
          <span class="name">{{ notification.name }}</span>
          <span class="action">has joined your group</span>
          <span class="notice club">{{ notification.group }}</span>
          <span :class="{ red: !notification.read }"></span>
        </p>
        <p class="time">{{ notification.created_at }}</p>
      </div>
      <div v-if="notification.event === 'comment'" class="flex">
        <p>
          <span class="name">{{ notification.name }}</span>
          <span class="action">commented on your picture</span>
          <span :class="{ red: !notification.read }"></span>
          <span class="time">{{ notification.created_at }}</span>
        </p>
        <img :src="notification.picture" />
      </div>
      <div v-if="notification.event === 'Left club'">
        <div>
          <p>
            <span class="name">{{ notification.name }}</span>
            <span class="action">left the group</span>
            <span class="notice club">{{ notification.group }}</span>
            <span :class="{ red: !notification.read }"></span>
          </p>
          <p class="time">{{ notification.created_at }}</p>
        </div>
      </div>
      <div v-if="notification.event === 'sent message'">
        <div>
          <p>
            <span class="name">{{ notification.name }}</span>
            <span class="action">sent you a private message</span>
          </p>
          <p class="time">{{ notification.created_at }}</p>
        </div>

        <p class="message">{{ notification.message }}</p>
      </div>
    </li>
  </ul>
</template>
