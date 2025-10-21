<script>
import axios from 'axios'

export default { 
  data() {
    return {
      moods: ["Happy", "Sad", "Angry"],
      posts: [],
      subject: "",
      entry: "",
      mood: "",
      outputMsg: ""
    }
  },

  computed: {
    baseUrl() {
      if (window.location.hostname === 'localhost') {
        return 'http://localhost:3000';
      } else {
        const codespace_host = window.location.hostname.replace('5173', '3000');
        return `https://${codespace_host}`;
      }
    }
  },

  methods: {
    async addPost() {
      try {
        const url = `${this.baseUrl}/addPost`; // adjust endpoint name if needed
        const response = await axios.get(url, {
          params: {
            subject: this.subject,
            entry: this.entry,
            mood: this.mood
          }
        });

        this.outputMsg = "✅ Post successfully added!";
        console.log(response.data);

      } catch (error) {
        this.outputMsg = "❌ Error adding post.";
        console.error(error);
      }
    }
  }
}
</script>

<template>
  <div class="table m-2">
    <h3>Add a New Blog Post</h3>

    <label>
      Subject:
      <input type="text" size="30" v-model="subject" required />
    </label>
    <br />

    <label>
      Entry:
      <br />
      <textarea cols="80" rows="5" v-model="entry" required></textarea>
    </label>
    <br />

    <label>
      Mood:
      <select v-model="mood">
        <option disabled value="">Select your mood</option>
        <option v-for="moodOption in moods" :key="moodOption">
          {{ moodOption }}
        </option>
      </select>
    </label>

    <br /><br />

    <button @click="addPost">Submit New Post</button>

    <p>{{ outputMsg }}</p>

    <hr />
    Click <router-link to="/ViewPosts/">here</router-link> to return to Main Page
  </div>
</template>
