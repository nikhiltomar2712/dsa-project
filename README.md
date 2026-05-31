# Real-Time Ride-Sharing Platform Simulator

A comprehensive single‑page web application that simulates a dynamic ride‑sharing service in a city grid. It efficiently matches riders with drivers using advanced data structures and algorithms, visualises the road network with real‑time traffic, and provides live analytics—all running in the browser.


## 🚀 Features

- **Interactive Map** – A 6×6 grid of 36 intersections with named locations (Central Park, Times Square, etc.).
- **Real-Time Matching** – Min‑Heap priority queue finds the nearest available driver based on estimated time of arrival (ETA).
- **Optimal Routing** – Dijkstra’s algorithm calculates the shortest path, factoring in per‑segment traffic density.
- **Traffic Simulation** – A Fenwick Tree (Binary Indexed Tree) tracks live traffic density on every road segment, affecting route costs.
- **Road Closures** – Union‑Find (Disjoint Set Union) handles dynamic road closures. Click any road on the map to close or reopen it; the system re‑routes and checks connectivity instantly.
- **Autocomplete Search** – A Trie indexes all location names for fast prefix‑based search.
- **Caching** – An LRU Cache stores frequently computed routes and driver‑rider matches to accelerate repeated lookups.
- **Analytics Dashboard** – Live statistics: completed rides, average wait/ride times, driver utilization, cache hit rate, and more.
- **Concurrent Ride Simulation** – Multiple riders can be queued, and drivers can be en‑route simultaneously.
- **Performance‑Focused** – All core operations run with well‑defined time and space complexities.

## 🧠 Data Structures & Their Roles

| Structure | Use Case | Key Operations (Time Complexity) |
|-----------|----------|----------------------------------|
| **Graph** (Adjacency List) | City road network (nodes = intersections, weighted edges = roads) | Edge lookup O(1), Dijkstra O((V+E) log V) |
| **Min‑Heap** (Priority Queue) | Matching nearest driver by ETA | Insert/Extract O(log D), D = number of available drivers |
| **Hash Map** (JavaScript `Map`) | Fast driver/rider lookups, node name → ID mapping | O(1) average |
| **Trie** | Autocomplete in location search | Insert O(k), Search O(p) (k = word length, p = prefix length) |
| **Fenwick Tree** (Binary Indexed Tree) | Real‑time traffic density updates and range queries | Update/Query O(log E), E = number of edges |
| **Union‑Find** (Disjoint Set Union) | Dynamic road closures and connectivity checks | Union/Find O(α(N)) amortized, N = number of nodes |
| **LRU Cache** | Store recently requested routes and matches | Get/Put O(1) |

## 🛠️ How to Run

1. **Download** the `index.html` file (or clone the repository).
2. **Open** it in any modern web browser (Chrome, Firefox, Edge, Safari).
3. No build tools, servers, or external dependencies required—everything is self‑contained.

> **Tip:** For a better experience, use a browser with hardware acceleration enabled.

## 🎮 Usage

### Simulation Controls
- **Speed Slider** – Adjust simulation speed (0.5× to 5×).
- **Spawn Rate** – Control how many new riders appear per minute.
- **Add Driver** – Manually place a new available driver at a random intersection.
- **Spawn Rider** – Instantly create a rider requesting a random trip.
- **Toggle Road Closure Mode** – When active, click any road segment on the map to close or reopen it. Closed roads are shown as dashed red lines.
- **Reset All** – Clears everything and restarts with 8 drivers.

### Map Interaction
- **Search Bar** – Start typing a location name (e.g., “Cen”, “Wall”). The Trie‑based autocomplete suggests matching intersections. Click a suggestion to highlight it on the map.
- **Hover** – Move the mouse over intersections to see their names. In closure mode, hovering over a road shows its status.
- **Click Roads** (only when “Closure Mode” is ON) – Toggle a road’s open/closed state. Drivers instantly recalculate their paths if affected.

### Live Visual Feedback
- 🟢 **Available Driver**
- 🟠 **Driver en route to pickup**
- 🔵 **Driver with rider on board**
- 🟡 **Waiting rider** (unmatched)
- 🔴 **Closed road**
- Road colour intensifies with traffic density (from blue‑green to reddish).

## 📊 Analytics Panel

The sidebar displays real‑time metrics:

- **Total Rides Completed**
- **Average Wait Time** (time from request to pickup)
- **Average Ride Time** (time from pickup to drop‑off)
- **Driver Utilization** (percentage of active time spent busy)
- **Active / Available Drivers**
- **Pending Riders** (waiting for a match)
- **LRU Cache Hit Rate** (indicates how often cached routes are reused)
- **Number of Closed Roads**

## 🧪 Customization

You can easily modify the simulation by editing the constants near the top of the `<script>` block (around line 1250):

```javascript
const GRID_ROWS = 6;          // Change grid size
const GRID_COLS = 6;
const INITIAL_DRIVERS = 8;    // Number of drivers at start
const LRU_CAPACITY = 200;     // Cache size
