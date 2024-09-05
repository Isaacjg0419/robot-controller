<template>
  <div class="robot-container">
    <div class="grid-container">
      <div class="grid">
        <div v-for="(cell, index) in 25" :key="index" class="cell" :class="{ robot: isRobotPosition(index) }">
          <div v-if="isRobotPosition(index)" class="robot-icon">{{ getDirectionIcon() }}</div>
        </div>
      </div>
    </div>
    <div class="controls">
      <button @click="rotateLeft" class="button">Rotate Left</button>
      <button @click="rotateRight" class="button">Rotate Right</button>
      <button @click="moveForward" class="button">Move Forward</button>
    </div>
    <div v-if="errorMessage" class="error-message">{{ errorMessage }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      gridSize: 5, 
      robot: {
        x: 0,
        y: 0,
        direction: "NORTH", 
      },
      directions: ["NORTH", "EAST", "SOUTH", "WEST"], // Directions
      errorMessage: "",
    };
  },
  methods: {
    // Check if robot is in the current position
    isRobotPosition(index) {
      const { x, y } = this.robot;
      const robotIndex = y * this.gridSize + x;
      return index === robotIndex;
    },
    // Get robot icon based on direction
    getDirectionIcon() {
      const icons = {
        NORTH: "↑",
        EAST: "→",
        SOUTH: "↓",
        WEST: "←",
      };
      return icons[this.robot.direction];
    },
    // Rotate the robot left
    rotateLeft() {
      const currentIndex = this.directions.indexOf(this.robot.direction);
      const newIndex = (currentIndex - 1 + this.directions.length) % this.directions.length;
      this.robot.direction = this.directions[newIndex];
    },
    // Rotate the robot right
    rotateRight() {
      const currentIndex = this.directions.indexOf(this.robot.direction);
      const newIndex = (currentIndex + 1) % this.directions.length;
      this.robot.direction = this.directions[newIndex];
    },
    // Move the robot forward
    moveForward() {
      const { x, y, direction } = this.robot;
      this.errorMessage = ""; // Clear previous error message
      switch (direction) {
        case "NORTH":
          if (y > 0) this.robot.y -= 1;
          else this.errorMessage = "Cannot move North!";
          break;
        case "EAST":
          if (x < this.gridSize - 1) this.robot.x += 1;
          else this.errorMessage = "Cannot move East!";
          break;
        case "SOUTH":
          if (y < this.gridSize - 1) this.robot.y += 1;
          else this.errorMessage = "Cannot move South!";
          break;
        case "WEST":
          if (x > 0) this.robot.x -= 1;
          else this.errorMessage = "Cannot move West!";
          break;
      }
    },
  },
};
</script>

<style scoped>
.robot-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.grid-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

.grid {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 10px;
  max-width: 500px;
}

.cell {
  aspect-ratio: 1 / 1;
  width: 100%;
  border: 2px solid #ddd;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #f8f8f8;
}

.robot {
  background-color: #d6e9f8;
}

.robot-icon {
  font-size: 24px;
  font-weight: bold;
}

.controls {
  display: flex;
  gap: 10px;
  margin-top: 10px;
}

.button {
  padding: 10px 15px;
  cursor: pointer;
  border: none;
  background-color: #004c6d;
  color: white;
  border-radius: 4px;
  transition: background-color 0.3s;
}

.button:hover {
  background-color: #006b94;
}

.error-message {
  color: red;
  font-weight: bold;
  margin-top: 10px;
}

@media (max-width: 600px) {
  .grid {
    grid-template-columns: repeat(5, 1fr);
  }

  .controls {
    flex-direction: column;
    gap: 5px;
  }

  .button {
    width: 100%;
  }
}
</style>
