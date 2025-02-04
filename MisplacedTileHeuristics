
import heapq

GOAL_STATE = [1, 2, 3, 4, 5, 6, 7, 8, 0]

# 1.2 Get the neighbors
def get_neighbors(state):
    neighbors = []
    blank_pos = state.index(0)
    row, col = divmod(blank_pos, 3)

    directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]  # up, down, left, right

    for drow, dcol in directions:
        new_row, new_col = row + drow, col + dcol

        if 0 <= new_row < 3 and 0 <= new_col < 3:
            new_blank_pos = new_row * 3 + new_col
            new_state = state[:]
            # Swap blank and adjacent tile
            new_state[blank_pos], new_state[new_blank_pos] = new_state[new_blank_pos], new_state[blank_pos]
            neighbors.append(new_state)

    return neighbors

# 1.3 misplaced tiles heuristic
def misplaced_tiles_heuristic(state):
    return sum(1 for i in range(len(state)) if state[i] != GOAL_STATE[i] and state[i] != 0)

# 1.4 A* search algorithm
def a_star_search(initial_state):
    open_list = []
    heapq.heappush(open_list, (misplaced_tiles_heuristic(initial_state), 0, initial_state, []))
    closed_list = set()
    
    while open_list:
        f, g, current_state, path = heapq.heappop(open_list)
        if current_state == GOAL_STATE:
            return path + [current_state]

        closed_list.add(tuple(current_state))

        for neighbor in get_neighbors(current_state):
            if tuple(neighbor) not in closed_list:
                g_new = g + 1
                f_new = g_new + misplaced_tiles_heuristic(neighbor)
                heapq.heappush(open_list, (f_new, g_new, neighbor, path + [current_state]))
    
    return None

# 1.5 print the state
def print_state(state):
    for i in range(0, 9, 3):
        print(state[i], state[i+1], state[i+2])
    print()

# 1.6 main function
def solve_puzzle(initial_state):
    print("Initial state:")
    print_state(initial_state)

    solution_path = a_star_search(initial_state)
    if solution_path:
        print("Solution path:")
        for step in solution_path:
            print_state(step)
    else:
        print("No solution found")

if __name__ == "__main__":
    initial_state = [1, 2, 3, 4, 0, 5, 6, 7, 8]
    solve_puzzle(initial_state)
