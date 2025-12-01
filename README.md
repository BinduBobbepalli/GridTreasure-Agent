# AI Agent Project

This repository contains a simple grid-world AI agent demonstration built using Python.

## Features
- Grid-based environment  
- Agent movement  
- Goal + hazard logic  
- Simple CLI simulation  

## How to Run




import random

GRID_SIZE = 6
AGENT = "A"
GOAL = "G"
HAZARD = "X"
EMPTY = "."


class GridWorld:
    def __init__(self):
        self.grid = [[EMPTY for _ in range(GRID_SIZE)] for _ in range(GRID_SIZE)]
        self.agent_pos = (0, 0)
        self.goal_pos = (4, 3)
        self.hazards = [(3, 4), (5, 2)]

        self.place_items()

    def place_items(self):
        x, y = self.agent_pos
        self.grid[x][y] = AGENT

        gx, gy = self.goal_pos
        self.grid[gx][gy] = GOAL

        for hx, hy in self.hazards:
            self.grid[hx][hy] = HAZARD

    def display(self):
        for row in self.grid:
            print(" ".join(row))
        print()

    def move_agent(self):
        moves = [(1, 0), (-1, 0), (0, 1), (0, -1)]
        dx, dy = random.choice(moves)
        x, y = self.agent_pos
        nx, ny = x + dx, y + dy

        if 0 <= nx < GRID_SIZE and 0 <= ny < GRID_SIZE:
            if self.grid[nx][ny] == HAZARD:
                print("Agent hit a hazard! ❌")
                return False
            if self.grid[nx][ny] == GOAL:
                print("Agent reached the goal! ⭐")
                return False

            self.grid[x][y] = EMPTY
            self.grid[nx][ny] = AGENT
            self.agent_pos = (nx, ny)

        return True


def run():
    env = GridWorld()
    env.display()

    while True:
        cont = env.move_agent()
        env.display()
        if not cont:
            break


if __name__ == "__main__":
    run()
