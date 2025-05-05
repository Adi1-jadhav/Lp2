# Lp2

# selection

def selection(arr):
    n = len(arr)
    for i in range(n):
        min_index = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_index]:
                min_index = j
        arr[i], arr[min_index] = arr[min_index], arr[i]
    return arr

if __name__ == "__main__":
    arr = [30, 40, 80, 56, 74, 24]
    res = selection(arr)
    print("After sorting:", res) 


#bfs

from collections import deque

def bfs_recursive(queue, visited, adj, bfs_result):
    if not queue:
        return
    node = queue.popleft()
    bfs_result.append(node)
    for neighbor in adj[node]:
        if not visited[neighbor]:
            visited[neighbor] = True
            queue.append(neighbor)
    bfs_recursive(queue, visited, adj, bfs_result)

def bfs_of_graph(v, adj):
    visited = [False] * v
    bfs_result = []
    queue = deque()

    # Start BFS from node 0
    visited[0] = True
    queue.append(0)

    bfs_recursive(queue, visited, adj, bfs_result)
    return bfs_result

if __name__ == "__main__":
    adj = [[] for _ in range(5)]
    adj[0].append(1)
    adj[0].append(4)
    adj[1].append(2)
    adj[1].append(3)
    adj[1].append(0)
    adj[2].append(1)
    adj[3].append(1)
    adj[4].append(0)

    result = bfs_of_graph(5, adj)
    for node in result:
        print("Traverse -", node)

#dfs


def dfs_of_graph(v, adj):
    visited = [False] * v
    dfs_result = []

    def dfs(node):
        visited[node] = True
        dfs_result.append(node)

        for neighbor in adj[node]:
            if not visited[neighbor]:
                dfs(neighbor)

    dfs(0)  # start DFS from node 0
    return dfs_result

if __name__ == "__main__":
    adj = [[] for _ in range(5)]
    adj[0].append(1)
    adj[0].append(4)
    adj[1].append(2)
    adj[1].append(3)
    adj[1].append(0)
    adj[2].append(1)
    adj[3].append(1)
    adj[4].append(0)

    result = dfs_of_graph(5, adj)
    for node in result:
        print("Traverse -", node)

# job scheduling

jobs = [
    {'id': 'A', 'deadline': 2, 'profit': 100},
    {'id': 'B', 'deadline': 1, 'profit': 19},
    {'id': 'C', 'deadline': 2, 'profit': 27},
    {'id': 'D', 'deadline': 1, 'profit': 25},
    {'id': 'E', 'deadline': 3, 'profit': 15}
]
# Sort jobs by profit (highest first)
jobs.sort(key=lambda x: x['profit'], reverse=True)

# Find max deadline
max_deadline = max(job['deadline'] for job in jobs)
slots = [None] * max_deadline

for job in jobs:
    for j in range(job['deadline']-1, -1, -1):
        if slots[j] is None:
            slots[j] = job['id']
            break
print("Scheduled Jobs:", [job for job in slots ])


#chatbot

def chatbot():
    print("Welcome to QuickShop Chatbot!")
    print("Type 'bye' to exit.\n")

    while True:
        user_input = input("You: ").lower()

        if "hello" in user_input or "hi" in user_input:
            print("Bot: Hello! How can I help you today?")
        elif "price" in user_input or "cost" in user_input:
            print("Bot: Could you please tell me which product you are interested in?")
        elif "laptop" in user_input:
            print("Bot: Our latest laptop starts at ₹49,999 with 8GB RAM and 512GB SSD.")
        elif "phone" in user_input:
            print("Bot: We have smartphones starting at ₹9,999. Do you want Android or iPhone?")
        elif "order status" in user_input or "track" in user_input:
            print("Bot: Please provide your order ID to track the status.")
        elif "bye" in user_input:
            print("Bot: Thank you for chatting with us. Have a great day!")
            break
        else:
            print("Bot: I'm sorry, I didn't understand that. Can you rephrase?")

# Run the chatbot
chatbot()

# nqueen

def solve_n_queens(n):
    board = [['.'] * n for _ in range(n)]
    cols = set()
    diag1 = set()  # row - col
    diag2 = set()  # row + col

    def backtrack(row):
        if row == n:
            for r in board:
                print(''.join(r))
            return True  # stop after first solution

        for c in range(n):
            if c in cols or (row - c) in diag1 or (row + c) in diag2:
                continue

            board[row][c] = 'Q'
            cols.add(c)
            diag1.add(row - c)
            diag2.add(row + c)

            if backtrack(row + 1):
                return True  # early stop after first solution

            board[row][c] = '.'
            cols.remove(c)
            diag1.remove(row - c)
            diag2.remove(row + c)

        return False  # no valid position in this row

    backtrack(0)

# Example usage
solve_n_queens(4)



#Expert system

# Simple Expert System for Employee Performance Evaluation

def evaluate_employee(punctuality, tasks_completed, teamwork, initiative):
    score = 0

    if punctuality == "yes":
        score += 1
    if tasks_completed == "yes":
        score += 1
    if teamwork == "yes":
        score += 1
    if initiative == "yes":
        score += 1

    print("\nEvaluation Result:")
    if score == 4:
        print("Excellent Performance")
    elif score == 3:
        print("Good Performance")
    elif score == 2:
        print("Average Performance")
    elif score == 1:
        print("Needs Improvement")
    else:
        print("Poor Performance")

# Main Program
print("Employee Performance Evaluation System")
print("Answer the following questions with 'yes' or 'no'.")

punctuality = input("Is the employee punctual? ").strip().lower()
tasks_completed = input("Does the employee complete tasks on time? ").strip().lower()
teamwork = input("Does the employee work well in a team? ").strip().lower()
initiative = input("Does the employee take initiative? ").strip().lower()

evaluate_employee(punctuality, tasks_completed, teamwork, initiative)


#prims

import heapq
def prim_mst(V,adj):
    visited=[False]*V
    min_heap=[]
    mst_weight=0

    heapq.heappush(min_heap,(0,0))
    while min_heap:
        weight,node=heapq.heappop(min_heap)

        if visited[node]:
            continue

        visited[node]=True
        mst_weight=mst_weight+weight

        for neighbour,weight in adj[node]:
            if not visited[neighbour]:
                heapq.heappush(min_heap,(weight,neighbour))

    return mst_weight

if __name__ == "__main__":
    V = 5  # number of vertices
    adj = [[] for _ in range(V)]

    # Add edges: adj[u].append((v, weight))
    adj[0].append((1, 2))
    adj[0].append((3, 6))
    adj[1].append((0, 2))
    adj[1].append((2, 3))
    adj[1].append((3, 8))
    adj[1].append((4, 5))
    adj[2].append((1, 3))
    adj[2].append((4, 7))
    adj[3].append((0, 6))
    adj[3].append((1, 8))
    adj[4].append((1, 5))
    adj[4].append((2, 7))

    total_weight = prim_mst(V, adj)
    print("Total weight of Minimum Spanning Tree:", total_weight)


        
