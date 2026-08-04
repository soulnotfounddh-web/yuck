Ex-1

from collections import deque 
graph = { 
    'A': ['B', 'C'], 
    'B': ['D', 'E'], 
    'C': ['F'], 
    'D': [], 
    'E': ['F'], 
    'F': [] 
} 
def bfs(graph, start): 
    visited = set() 
    queue = deque([start]) 
    visited.add(start) 
    while queue: 
        node = queue.popleft() 
        print(node, end=" ") 
        for neighbor in graph[node]: 
            if neighbor not in visited: 
                visited.add(neighbor) 
                queue.append(neighbor) 
 
bfs(graph, 'A')


Ex-2

graph = { 
    'A': ['B', 'C'], 
    'B': ['D', 'E'], 
    'C': ['F'], 
    'D': [], 
    'E': [], 
    'F': [] 
}  
visited = set() 
def dfs(node): 
    if node not in visited: 
        print(node, end=" ") 
        visited.add(node) 
        for neighbor in graph[node]: 
            dfs(neighbor) 
dfs('A') 


Ex-3

board = [' ' for x in range(9)] 
def display(): 
    print(board[0], "|", board[1], "|", board[2]) 
    print("--|---|--") 
    print(board[3], "|", board[4], "|", board[5]) 
    print("--|---|--") 
    print(board[6], "|", board[7], "|", board[8]) 
def check_winner(player): 
    win_positions = [ 
        [0,1,2], [3,4,5], [6,7,8], 
        [0,3,6], [1,4,7], [2,5,8], 
        [0,4,8], [2,4,6]]  
    for pos in win_positions: 
        if board[pos[0]] == board[pos[1]] == board[pos[2]] == player: 
            return True 
    return False 
player = 'X' 
for turn in range(9): 
    display() 
    move = int(input(f"Player {player}, enter position (0-8): ")) 
    if board[move] == ' ': 
        board[move] = player 
        if check_winner(player): 
            display() 
            print(f"Player {player} wins!") 
            break 
        player = 'O' if player == 'X' else 'X' 
    else: 
        print("Position already filled") 
else: 
    print("Game Draw") 



Ex-4

from collections import deque
def solve(b):
    s = sum(b,[])
    goal = list(range(9))
    if s == goal:
        print("Final Matrix:")
        for i in range(0, 9, 3):
            print(goal[i:i+3])
        return 0
    m = [[1,3],[0,2,4],[1,5],[0,4,6],[1,3,5,7],[2,4,8],[3,7],
         [4,6,8],[5,7]]
    q = deque([(s,0)])
    v = set()
    while q:
        t,c = q.popleft()
        if tuple(t) in v:
            continue
        v.add(tuple(t))
        z = t.index(0)
        for i in m[z]:
            n = t[:]
            n[z],n[i] = n[i],n[z]
            if n == goal:
                print("Final Matrix:")
                for j in range(0, 9, 3):
                    print(n[j:j+3])
                return c+1
            q.append((n,c+1))
    return -1
moves = solve([[3,1,2],[4,7,5],[6,8,0]])
print("Minimum moves:",moves)



Ex-5

jug1 = 4 
jug2 = 3 
x = 0 
y = 0 
print("Initial State:", x, y) 
y = jug2 
print("Fill Jug2:", x, y) 
x = y 
y = 0 
print("Pour Jug2 into Jug1:", x, y) 
y = jug2 
print("Fill Jug2 again:", x, y) 
y = y - (jug1 - x) 
x = jug1 
print("Final State:", x, y) 



Ex-6

from itertools import permutations 
graph = { 
    'A': {'B': 10, 'C': 15, 'D': 20}, 
    'B': {'A': 10, 'C': 35, 'D': 25}, 
    'C': {'A': 15, 'B': 35, 'D': 30}, 
    'D': {'A': 20, 'B': 25, 'C': 30} 
} 
cities = list(graph.keys()) 
min_path = None 
min_cost = float('inf') 
for path in permutations(cities): 
    cost = 0 
    for i in range(len(path)-1): 
        cost += graph[path[i]][path[i+1]] 
    cost += graph[path[-1]][path[0]] 
    if cost < min_cost: 
        min_cost = cost 
        min_path = path 
print("Minimum Path:", min_path) 
print("Minimum Cost:", min_cost) 


Ex-7

def tower(n, source, auxiliary, destination): 
    if n == 1: 
        print("Move disk 1 from", source, "to", destination) 
        return 
    tower(n-1, source, destination, auxiliary) 
    print("Move disk", n, "from", source, "to", destination) 
    tower(n-1, auxiliary, source, destination) 
tower(3, 'A', 'B', 'C')








