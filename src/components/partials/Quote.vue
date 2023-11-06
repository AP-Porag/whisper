<template>
  <div class="bg-white p-6 rounded-lg shadow-lg">
    <h2 class="text-2xl font-bold mb-2 text-gray-800">Card with no image</h2>
    <p class="text-gray-700">This is my cool new card!</p>
    <p class="text-gray-700">Post by : user name</p>
    <p class="text-gray-700">Author : some name</p>

    <div class="rating-component">
      <div class="rating-buttons">
        <a class="button like">
          <div class="rate-icon">
            <svg viewBox="0 0 24 24" preserveAspectRatio="xMidYMid meet" focusable="false" style="pointer-events: none; display: block; width: 100%; height: 100%;"><g class="style-scope yt-icon">
              <path d="M1 21h4V9H1v12zm22-11c0-1.1-.9-2-2-2h-6.31l.95-4.57.03-.32c0-.41-.17-.79-.44-1.06L14.17 1 7.59 7.59C7.22 7.95 7 8.45 7 9v10c0 1.1.9 2 2 2h9c.83 0 1.54-.5 1.84-1.22l3.02-7.05c.09-.23.14-.47.14-.73v-1.91l-.01-.01L23 10z" class="style-scope yt-icon"></path>
            </g></svg>
          </div>
          <div id="rate-count-positive">0</div>
        </a>

        <a class="button dislike">
          <div class="rate-icon">
            <svg viewBox="0 0 24 24" preserveAspectRatio="xMidYMid meet" focusable="false" style="pointer-events: none; display: block; width: 100%; height: 100%;"><g class="style-scope yt-icon">
              <path d="M15 3H6c-.83 0-1.54.5-1.84 1.22l-3.02 7.05c-.09.23-.14.47-.14.73v1.91l.01.01L1 14c0 1.1.9 2 2 2h6.31l-.95 4.57-.03.32c0 .41.17.79.44 1.06L9.83 23l6.59-6.59c.36-.36.58-.86.58-1.41V5c0-1.1-.9-2-2-2zm4 0v12h4V3h-4z" class="style-scope yt-icon"></path>
            </g></svg>
          </div>
          <div id="rate-count-negative">0</div>
        </a>
      </div>
      <!-- 	<div class="sentiment">
          <div id="positive-bar"></div>
        </div> -->
    </div>
  </div>
</template>

<script>
export default {
  name: "Quote"
}
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@500&display=swap");

body {
  background: #181818;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100vw;
}

.rating-component {
  max-width: 150px;
  display: flex;
  flex-direction: column;

  .rating-buttons {
    display: flex;
    flex-direction: row;
    margin-bottom: 15px;
    justify-content: space-between;

    .button {
      display: flex;
      align-items: center;
      cursor: pointer;
      color: #909090;

      &:first-child {
        margin-right: 1em;
      }

      .rate-icon {
        margin-right: 5px;

        svg {
          fill: #909090;
        }
      }

      #rate-count-positive,
      #rate-count-negative {
        font-size: 13px;
        text-transform: uppercase;
        user-select: none;
      }
    }
  }

  .sentiment {
    height: 2.5px;
    width: 100%;
    background: #606060;
    position: relative;

    #positive-bar {
      position: absolute;
      background: #53a7ff;
      height: inherit;
    }
  }

  .rate-icon {
    width: 20px;
  }
}
</style>