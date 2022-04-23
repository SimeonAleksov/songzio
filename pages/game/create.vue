<template>
  <div>
    <h1>Choose a category:</h1>
    <ul class="image-list-small">
      <li>
        <img src="../../assets/images/albums/brkovi_1.jpg" />
        <div class="details">
          <h3><span>In the subway</span></h3>
          <p class="image-author">Matt Stone</p>
        </div>
      </li>
      <li>
        <img src="../../assets/images/albums/brkovi_2.jpg" />
        <div class="details">
          <h3><span>Industrial</span></h3>
          <p class="image-author">Earnest Leming</p>
        </div>
      </li>
      <li>
        <img src="../../assets/images/albums/brkovi_3.jpg" />
        <div class="details">
          <h3><span >When in Rome..</span></h3>
          <p class="image-author">Edward Flint</p>
        </div>
      </li>
      <li>
        <img src="../../assets/images/albums/mortal_kombat_1.jpg" />
        <div class="details">
          <h3><span>Mountain Top</span></h3>
          <p class="image-author">Rick Alpine</p>
        </div>
      </li>
      <li>
        <img src="../../assets/images/albums/bad_copy_1.jpg" />
        <div class="details">
          <h3><span>Mountain Top</span></h3>
          <p class="image-author">Rick Alpine</p>
        </div>
      </li>
      <li>
        <img src="../../assets/images/albums/vojko_v_1.jpg" />
        <div class="details">
          <h3><span>Mountain Top</span></h3>
          <p class="image-author">Rick Alpine</p>
        </div>
      </li>
      <li>
        <img src="../../assets/images/albums/challe_salle_1.jpg" />
        <div class="details">
          <h3><span>Mountain Top</span></h3>
          <p class="image-author">Rick Alpine</p>
        </div>
      </li>
    </ul>
    <div>
      <Button>Go back</Button>
      <Button :style-class="style" @click="handleCreate"> Create a game </Button>
    </div>
  </div>
</template>

<script>
import Button from "../../components/shared/Button";
export default {
  name: "create",
  components: { Button },
  data() {
    return {
      style: "pulse",
      connection: null,
      roomId: this.generateRoomId(),
    };
  },
  created() {
    this.connection = new WebSocket("ws://localhost:5000/ws");
    this.connection.onopen = () => {
      this.sendMessage(
        {
          action: 'subscribe',
          topic: this.roomId,
        }
      );
    };
    this.connection.onmessage = (message) => {
      console.log(message);
    };
  },
  beforeRouteLeave(to, from, next) {
    this.connection.close();
    next();
  },
  methods: {
    sendMessage(message) {
      this.connection.send(JSON.stringify(message));
    },
    generateRoomId() {
      return Math.random().toString(36).slice(2, 12);
    },
    handleCreate() {
      // this.$router.push({ path: '/game', params: { id: this.roomId } })
      this.$router.push({ name: 'game-id', params: { id: this.roomId } })
    }
  },
};
</script>

<style scoped>
.image-list-small {
  font-family: Arial, Helvetica, sans-serif;
  margin: 0 auto;
  text-align: center;
  max-width: 640px;
  padding: 0;
}

.image-list-small li {
  display: inline-block;
  width: 181px;
  margin: 0 12px 30px;
}

/* Photo */

.image-list-small li > img {
  display: block;
  text-decoration: none;
  background-size: cover;
  background-repeat: no-repeat;
  height: 137px;
  margin: 0;
  padding: 0;
}

.image-list-small .details {
  margin-top: 13px;
}

/* Title */

.image-list-small .details h3 {
  display: block;
  font-size: 12px;
  margin: 0 0 3px 0;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.image-list-small .details h3 a {
  color: #303030;
  text-decoration: none;
}

.image-list-small .details .image-author {
  display: block;
  color: #f1f1f1;
  font-size: 11px;
  font-weight: normal;
  margin: 0;
}
</style>
