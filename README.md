# 🧩 Maze Agent Exercise

## Overview

In this exercise, you will build a simple software agent (a program) that can navigate a maze by interacting with a REST API. The agent will not see the whole maze at once—it will only know its current position and the status of the four adjacent cells (up, down, left, right) after each move.

Your goal is to write a client that can reach the exit of the maze by making a series of valid moves.

---

## API Endpoints

### 1. Start a New Maze Session

**Request:**  
`POST /api/maze/start`

**Response:**
```json
{
  "sessionId": "string",
  "position": [0, 0],
  "surroundings": {
    "up": "wall",
    "down": "wall",
    "left": "wall",
    "right": "free space"
  }
}
```
- `sessionId`: Unique ID for your game session.  
- `maze`: The full maze layout (for debugging; your agent should not use this to cheat!).  
- `position`: Your starting coordinates.  
- `surroundings`: What is in each direction from your current position.

---

### 2. Make a Move

**Request:**  
`POST /api/maze/move`

**Body:**
```json
{
  "sessionId": "string",
  "direction": "up" | "down" | "left" | "right"
}
```

**Response:**
```json
{
  "position": [x, y],
  "status": "ok" | "wall" | "end",
  "surroundings": {
    "up": "wall",
    "down": "free space",
    "left": "wall",
    "right": "exit"
  }
}
```
- `position`: Your new position (or unchanged if you hit a wall).
- `status`:  
  - `"ok"`: Move successful.  
  - `"wall"`: You hit a wall; position unchanged.  
  - `"end"`: You reached the exit!
- `surroundings`: What is in each direction from your new position.

---

## Your Task

1. **Start a new session** by calling `/api/maze/start`. Save the `sessionId`.
2. **Write a program (agent)** that:
    - Sends moves to `/api/maze/move` using the `sessionId`.
    - Decides which direction to move based only on the `surroundings` field in the response.
    - Repeats until it reaches the exit (`status: "end"`).
3. **(Optional)**: Try to implement a smarter agent that finds the shortest path!

---




## Rules

- You may only use the `surroundings` field to decide your next move.
- Only one move is allowed per API call.
- If you hit a wall, your position does not change.
- The goal is to reach the exit cell (`"E"`).

---

## Challenge

- Can you write an agent that always finds the exit, no matter where it starts?

---
