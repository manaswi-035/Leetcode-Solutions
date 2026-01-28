
# LeetCode 3651 - Minimum Cost Path with Teleportations (Java)

## ✅ Problem Summary
You are given an `m x n` grid and an integer `k`.

- Start at the top-left cell `(0,0)`
- Reach the bottom-right cell `(m-1,n-1)`
- You can move only **Right** or **Down** using **Normal Moves**
- You can also use **Teleportation** at most `k` times

### Normal Move
From `(i,j)` → `(i+1,j)` or `(i,j+1)`  
Cost = value of the cell you move into.

### Teleportation
From any cell `(i,j)` → any cell `(x,y)` where:

`grid[x][y] <= grid[i][j]`

Teleportation cost = **0**  
(You do not pay destination cell value during teleport)

✅ Goal: Find the **minimum total cost** to reach the destination.

---

## 💡 Concept / Approach Used

This problem is solved using **Dynamic Programming (DP)** with **Fenwick Tree (Binary Indexed Tree - BIT)** to handle teleportation efficiently.

### 1️⃣ Dynamic Programming Idea
We maintain DP states based on how many teleports are used.

Let:
`dp[t][i][j]` = minimum cost to reach cell `(i,j)` using at most `t` teleportations.

For each `t` (0 to k), we compute the best cost.

---

## ✅ Two ways to reach a cell

### ✅ A) By Normal Move (Paid)
From top or left cell:

`dp[t][i][j] = min(dp[t][i-1][j], dp[t][i][j-1]) + grid[i][j]`

---

### ✅ B) By Teleportation (Free)
Teleport is allowed only when:

destination value ≤ source value

So for a destination cell `(i,j)`, we want the minimum:

`dp[t-1][source]`

among all cells where `grid[source] >= grid[i][j]`

Teleport cost = `0`, so:

`dp[t][i][j] = min(dp[t][i][j], bestTeleportSourceCost)`

---

## ⚡ Why Fenwick Tree (BIT) is used?
Teleportation can come from **any cell**, so checking all sources for every destination would be too slow.

To make it fast:
- We use **coordinate compression** of grid values
- We use a **Fenwick Tree** to quickly get the minimum DP cost among valid teleport source cells

This reduces the time complexity drastically.

---

## ✅ Time & Space Complexity
- Time Complexity: approximately **O(k * m * n * log(m*n))**
- Space Complexity: **O(m*n)** (only two DP layers are stored)
