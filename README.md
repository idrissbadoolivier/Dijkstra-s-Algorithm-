# 🛣️ Implementing Dijkstra's Algorithm in JavaScript

## 🎯 Objective

The goal of this task is to implement **Dijkstra’s Algorithm** in JavaScript to find the **shortest path** in a weighted graph. This exercise builds a strong foundation in graph algorithms and showcases how such algorithms solve real-world problems like routing, GPS navigation, and network optimization.

---

## 📚 What is Dijkstra's Algorithm?

Dijkstra’s algorithm is a **greedy algorithm** that solves the **single-source shortest path problem** for a graph with non-negative edge weights.  
It works by:
- Assigning a tentative distance value to every node (initially Infinity, except the start node which is 0),
- Exploring the nearest unvisited node,
- Updating the distances to its neighbors,
- Repeating until all nodes have been visited or the shortest paths are found.

---

## 📝 Problem Statement

You are given a weighted graph represented as an object:

```js
const graph = {
  'A': { 'B': 4, 'C': 2 },
  'B': { 'A': 4, 'C': 5, 'D': 10 },
  'C': { 'A': 2, 'B': 5, 'D': 3 },
  'D': { 'B': 10, 'C': 3 }
};
```

Implement a JavaScript function:

```js
---

## 💡 Solution

Below is a working JavaScript implementation of Dijkstra’s algorithm:

```js
function dijkstra(graph, start) {
  const distances = {};
  const visited = new Set();
  const priorityQueue = new Map();

  // Initialize distances
  for (let vertex in graph) {
    distances[vertex] = Infinity;
  }
  distances[start] = 0;
  priorityQueue.set(start, 0);

  while (priorityQueue.size > 0) {
    // Find the node with the smallest distance
    let currentVertex = null;
    let smallestDistance = Infinity;

    for (let [vertex, distance] of priorityQueue.entries()) {
      if (distance < smallestDistance) {
        smallestDistance = distance;
        currentVertex = vertex;
      }
    }

    priorityQueue.delete(currentVertex);
    visited.add(currentVertex);

    // Update distances to neighbors
    for (let neighbor in graph[currentVertex]) {
      if (!visited.has(neighbor)) {
        let newDistance = distances[currentVertex] + graph[currentVertex][neighbor];
        if (newDistance < distances[neighbor]) {
          distances[neighbor] = newDistance;
          priorityQueue.set(neighbor, newDistance);
        }
      }
    }
  }

  return distances;
}
```

```

The function should return the shortest distances from the `start` node to all other nodes.

---

## ✅ Expected Output

Calling the function like this:

```js
console.log(dijkstra(graph, 'A'));
```

Should return:

```js
{
  A: 0,
  B: 4,
  C: 2,
  D: 5
}
```


---

## 🧪 Example Run

```js
const graph = {
  'A': { 'B': 4, 'C': 2 },
  'B': { 'A': 4, 'C': 5, 'D': 10 },
  'C': { 'A': 2, 'B': 5, 'D': 3 },
  'D': { 'B': 10, 'C': 3 }
};

console.log(dijkstra(graph, 'A'));
// Output: { A: 0, B: 4, C: 2, D: 5 }
```

---

## 📈 Time Complexity

- **O(V²)** using a simple priority queue (as in this example).
- Can be improved to **O((V + E) log V)** using a binary heap or priority queue implementation.

---

## 📘 What I Learned

- How to work with **graphs** in JavaScript.
- How to apply **greedy algorithms** for pathfinding.
- Importance of **data structures** like maps, sets, and queues in algorithm efficiency.
- How **Dijkstra's algorithm** is used in real-world apps like Google Maps, logistics, and networking.

---

## 🙋‍♂️ Further Improvements

- Add path reconstruction to track the actual route, not just distances.
- Replace the `Map` with a real priority queue for better performance.
- Extend the function to work with directed or undirected graphs dynamically.

---

## 📎 References

- [Dijkstra’s Algorithm - GeeksforGeeks](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-priority_queue-stl/)
- [JavaScript Graph Implementation - FreeCodeCamp](https://www.freecodecamp.org/news/implementing-dijkstras-shortest-path-algorithm-in-javascript-8c5e5d3e5f46/)

---

**©️ Written by a student passionate about algorithms and clean JavaScript code.**
