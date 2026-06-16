# ⬡ MST Friend Recommendation System

A social network visualization tool built with **Flask** and **HTML5 Canvas** that uses **Minimum Spanning Tree (MST)** algorithms to suggest friend recommendations based on graph connectivity.

---

## 🚀 Features

- **Interactive Graph Visualization** — 20 users rendered in a circular layout on an HTML5 canvas
- **Prim's Algorithm** — Step-by-step MST construction starting from node 0
- **Kruskal's Algorithm** — Step-by-step MST construction via sorted edge selection
- **Step-by-step Mode** — Navigate MST construction forward/backward one edge at a time
- **Friend Recommendations** — Suggests friends-of-friends based on the computed MST
- **User Management** — Add new users with custom connections
- **Friendship Management** — Add, update, or delete edges between users with selectable weights

---

## 🛠️ Tech Stack

| Layer     | Technology              |
|-----------|-------------------------|
| Backend   | Python, Flask           |
| Frontend  | HTML5 Canvas, Vanilla JS |
| Rendering | Server-side Jinja2 templating |

---

## 📦 Installation

```bash
# Clone the repository
git clone <your-repo-url>
cd mst-friend-recommendation

# Install dependencies
pip install flask

# Run the app
python app.py
```

App runs at: `http://127.0.0.1:5000`

---

## 🗂️ Project Structure

```
.
├── app.py          # Flask backend — routes, graph data, MST logic
└── README.md
```

> The HTML, CSS, and JavaScript are all embedded inside `app.py` via a Jinja2 template string.

---

## 🔌 API Endpoints

| Method | Route          | Description                          |
|--------|----------------|--------------------------------------|
| GET    | `/`            | Render the main graph UI             |
| POST   | `/add_edge`    | Add a friendship edge                |
| POST   | `/update_edge` | Update the weight of an existing edge |
| POST   | `/delete_edge` | Remove a friendship edge             |
| POST   | `/add_user`    | Add a new user with connections      |
| POST   | `/recommend`   | Get friend recommendations via MST   |

### `/recommend` — Request Body

```json
{
  "user": 0,
  "algo": "prim",
  "mstEdges": [{ "source": 0, "target": 1, "weight": 3 }, ...]
}
```

**Response:**

```json
{
  "recommendations": [{ "id": 4, "name": "Sara" }],
  "algorithm": "prim"
}
```

---

## 📊 Graph Details

- **Nodes:** 20 users arranged in a circle
- **Edges:** 60 randomly weighted edges (weights 1–10)
- Initial edges guarantee connectivity via a linear chain, with random edges added up to 60

---

## 🎨 Visual Legend

| Color         | Meaning                          |
|---------------|----------------------------------|
| 🔵 Blue node  | Unselected user                  |
| 🟠 Orange node | Currently selected user          |
| 🟢 Green node | Directly connected to selected   |
| — Gray edge   | Regular friendship               |
| — Orange edge | MST edge                         |
| — Blue edge   | Edge connected to selected node  |

---

## 🧠 Algorithms

### Prim's Algorithm
Greedy approach — starts at node 0, always picks the minimum-weight edge crossing the visited/unvisited boundary.

### Kruskal's Algorithm
Sort all edges by weight, then union nodes using a Union-Find structure, skipping edges that would create a cycle.

### Friend Recommendation Logic
After MST is computed, for a selected user:
1. Find all direct MST neighbors
2. Find all neighbors-of-neighbors
3. Recommend nodes that are **not** already direct neighbors

---

## ⚠️ Limitations

- Graph data is **in-memory only** — restarting the server resets all users and edges
- No user authentication or persistent storage
- Node layout recalculates on every user addition (positions shift)

---

## 📄 License

MIT License — free to use and modify.
