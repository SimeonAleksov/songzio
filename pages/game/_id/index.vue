<template>
  <div class="container">
    <h1>
      Current room: {{ id }}
    </h1>
    <Loading v-show="isLoadingNext"/>
    <div class="wrapper">
      <ul class="img-grid">
        <li v-for="user in users">
          <div class="overlay-container img-with-text" :data-overlay-text="user.user">
            <img :src="user.img" alt="Image capture goes here 01" class="overlay-img" />
            <span class="img-grid__text">{{ user.user }} - {{ user.score}}</span>
          </div>
        </li>
      </ul>
    </div>
    <div class="container__answers">
      <Button v-for="(item, idx) in answers" class="container__button" :style-class="styleClass" :key="idx">{{ item }}</Button>
    </div>
  </div>
</template>

<script>
import Button from "../../../components/shared/Button";
import Loading from "../../../components/shared/Loading";
export default {
  name: "id",
  components: {Loading, Button},
  async asyncData({ params }) {
    const id = params.id // When calling /abc the slug will be "abc"
    return { id }
  },
  data() {
    return {
      isLoadingNext: false,
      styleClass: 'pulse',
      answers: [
        'Answer 1',
        'Answer 2',
        'Answer 3',
        'Answer 4',
      ],
      users: [
        {
          user: 'user1',
          score: 0,
          img: 'https://api.minimalavatars.com/avatar/user1/png',
        },
        {
          user: 'user2',
          score: 0,
          img: 'https://api.minimalavatars.com/avatar/user2/png',
        },
        {
          user: 'user3',
          score: 0,
          img: 'https://api.minimalavatars.com/avatar/user3/png',
        },
        {
          user: 'user4',
          score: 0,
          img: 'https://api.minimalavatars.com/avatar/user4/png',
        }
      ]
    }
  },
  mounted() {
    console.log(this.$router)
  }
}
</script>

<style scoped lang="scss">
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  &__answers {
    display: flex;
    flex-wrap: wrap;
    margin-top: 25%;
  }
  &__button {
    flex: 40%;
    width: 100%;
  }
  &__avatars {
    width: 150px;
    height: 150px;
    margin: 5px
  }
  &__avatar-list  {
    display: flex;
  }
}

.wrapper {
  max-width: 80em;
  margin-top: 2rem;
  li {
    display: inline-block;
    overflow: hidden;
    max-height: 200px;
  }
  img {
    max-width: 200px;
  }
  .overlay-container {
    display: flex;
    flex-direction: column-reverse;
    position: relative;
    &::before {
      content: attr(data-overlay-text);
      font: 1em/1.5em 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      position: absolute;
      z-index: 1;
      /*On top of parent*/
      top: 40%;
      width: 100%;
      text-align: center;
      color: #fff;
      background: rgba(128, 128, 128, 0.80);
      opacity: 0;
      -moz-transform: translateY(0);
      -ms-transform: translateY(0);
      -o-transform: translateY(0);
      -webkit-transform: translateY(0);
      transform: translateY(0);
      -moz-transition: all 0.3s;
      -o-transition: all 0.3s;
      -webkit-transition: all 0.3s;
      transition: all 0.3s;
    }
    &:hover::before {
      opacity: 1;
      -moz-transform: translateY(20px);
      -ms-transform: translateY(20px);
      -o-transform: translateY(20px);
      -webkit-transform: translateY(20px);
      transform: translateY(20px);
    }
    .overlay-img {
      -moz-transform: scale(1);
      -ms-transform: scale(1);
      -o-transform: scale(1);
      -webkit-transform: scale(1);
      transform: scale(1);
      -moz-transition: all 0.3s;
      -o-transition: all 0.3s;
      -webkit-transition: all 0.3s;
      transition: all 0.3s;
    }
    &:hover .overlay-img {
      -moz-transform: scale(1.2);
      -ms-transform: scale(1.2);
      -o-transform: scale(1.2);
      -webkit-transform: scale(1.2);
      transform: scale(1.2);
    }
  }
}

.img-grid__text {
  align-self: center;
}
</style>
