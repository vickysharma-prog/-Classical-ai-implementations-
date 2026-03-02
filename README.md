<div align="center">



\# 🧠 Classical AI Implementations



\[!\[Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge\&logo=python\&logoColor=white)](https://python.org)

\[!\[Pygame](https://img.shields.io/badge/Pygame-2.0+-00D000?style=for-the-badge\&logo=python\&logoColor=white)](https://pygame.org)

\[!\[License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)

\[!\[PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen?style=for-the-badge)](CONTRIBUTING.md)



\*\*Production-ready implementations of classical AI algorithms\*\*



\*Search • Game Theory • Knowledge Representation • Probabilistic Reasoning\*



\[Explore Projects](#-projects) • \[View Demo](#-demos) • \[Get Started](#-quick-start)



---



</div>



\## 📋 Table of Contents



\- \[About](#-about)

\- \[Projects](#-projects)

&nbsp; - \[BFS Actor Connections](#1-bfs-actor-connections)

&nbsp; - \[Minimax Tic-Tac-Toe](#2-minimax-tic-tac-toe)

\- \[Demos](#-demos)

\- \[Architecture](#-architecture)

\- \[Algorithms Deep Dive](#-algorithms-deep-dive)

\- \[Upcoming Projects](#-upcoming-projects)

\- \[Tech Stack](#-tech-stack)

\- \[Quick Start](#-quick-start)

\- \[Contributing](#-contributing)

\- \[References](#-references)

\- \[License](#-license)

\- \[Author](#-author)



---



\## 🎯 About



This repository contains \*\*production-quality implementations\*\* of fundamental AI algorithms. Each project demonstrates core concepts in artificial intelligence with clean, well-documented code.



\### Why This Repository?



| Feature | Description |

|---------|-------------|

| 📚 \*\*Educational\*\* | Detailed explanations with algorithm visualizations |

| 🏗️ \*\*Well-Structured\*\* | Clean architecture following best practices |

| 📖 \*\*Documented\*\* | Comprehensive documentation for each algorithm |

| 🧪 \*\*Tested\*\* | Verified implementations with sample datasets |

| 🚀 \*\*Extensible\*\* | Easy to extend and modify for your needs |



\### Concepts Covered

┌─────────────────────────────────────────────────────────────────┐

│ ARTIFICIAL INTELLIGENCE │

├─────────────────┬─────────────────┬─────────────────────────────┤

│ SEARCH │ GAME THEORY │ KNOWLEDGE \& PROBABILITY │

├─────────────────┼─────────────────┼─────────────────────────────┤

│ • BFS │ • Minimax │ • Propositional Logic │

│ • DFS │ • Alpha-Beta │ • Bayesian Networks │

│ • A\* Search │ • Expectimax │ • Markov Chains │

│ • Greedy Search │ • Game Trees │ • Constraint Satisfaction │

└─────────────────┴─────────────────┴─────────────────────────────┘



text





---



\## 🚀 Projects



\### 1. BFS Actor Connections



> \*\*Six Degrees of Separation\*\* — Find the shortest path between any two actors through shared movies.



<table>

<tr>

<td width="50%">



\#### 📝 Problem Statement



Given two actors, find the shortest sequence of movies that connects them. For example:

Tom Hanks → Kevin Bacon



Path Found:



Tom Hanks ─\[Apollo 13]─→ Kevin Bacon

Degrees of Separation: 1



text





</td>

<td width="50%">



\#### 📊 Complexity Analysis



| Metric | Value |

|--------|-------|

| \*\*Algorithm\*\* | Breadth-First Search |

| \*\*Time\*\* | O(V + E) |

| \*\*Space\*\* | O(V) |

| \*\*Optimality\*\* | ✅ Guaranteed shortest path |

| \*\*Completeness\*\* | ✅ Finds solution if exists |



</td>

</tr>

</table>



\#### 🔍 How BFS Works

text



&nbsp;               ┌─────────────┐

&nbsp;               │   START     │

&nbsp;               │  (Actor A)  │

&nbsp;               └──────┬──────┘

&nbsp;                      │

&nbsp;         ┌────────────┼────────────┐

&nbsp;         ▼            ▼            ▼

&nbsp;    ┌────────┐   ┌────────┐   ┌────────┐

&nbsp;    │ Movie1 │   │ Movie2 │   │ Movie3 │

&nbsp;    └───┬────┘   └───┬────┘   └───┬────┘

&nbsp;        │            │            │

&nbsp; ┌──────┴──────┐     │     ┌──────┴──────┐

&nbsp; ▼             ▼     ▼     ▼             ▼

┌───────┐ ┌───────┐ ... ┌───────┐ ┌───────┐

│Actor X│ │Actor Y│ │Actor Z│ │ GOAL! │

└───────┘ └───────┘ └───────┘ └───────┘



BFS explores level by level → guarantees shortest path



text





\#### 💻 Implementation



```python

def shortest\_path(source, target):

&nbsp;   """

&nbsp;   Find shortest path between two actors using BFS.

&nbsp;   

&nbsp;   Args:

&nbsp;       source: Starting actor's ID

&nbsp;       target: Goal actor's ID

&nbsp;   

&nbsp;   Returns:

&nbsp;       List of (movie\_id, actor\_id) tuples representing path

&nbsp;       None if no path exists

&nbsp;   """

&nbsp;   # Initialize frontier with starting position

&nbsp;   frontier = QueueFrontier()

&nbsp;   start = Node(state=source, parent=None, action=None)

&nbsp;   frontier.add(start)

&nbsp;   

&nbsp;   # Track explored states to avoid cycles

&nbsp;   explored = set()

&nbsp;   

&nbsp;   while not frontier.empty():

&nbsp;       # Get next node from queue (FIFO)

&nbsp;       node = frontier.remove()

&nbsp;       

&nbsp;       # Goal test

&nbsp;       if node.state == target:

&nbsp;           return reconstruct\_path(node)

&nbsp;       

&nbsp;       # Mark as explored

&nbsp;       explored.add(node.state)

&nbsp;       

&nbsp;       # Expand neighbors

&nbsp;       for movie\_id, actor\_id in neighbors\_for\_person(node.state):

&nbsp;           if actor\_id not in explored and not frontier.contains\_state(actor\_id):

&nbsp;               child = Node(state=actor\_id, parent=node, action=movie\_id)

&nbsp;               frontier.add(child)

&nbsp;   

&nbsp;   return None  # No path exists

📁 Project Structure

text



search-algorithms/bfs-actor-connections/

├── degrees.py          # Main BFS implementation

├── util.py             # Node, StackFrontier, QueueFrontier classes

└── data/

&nbsp;   ├── small/          # Test dataset (~100 actors)

&nbsp;   │   ├── movies.csv

&nbsp;   │   ├── people.csv

&nbsp;   │   └── stars.csv

&nbsp;   └── large/          # Full IMDb dataset (~500K actors)

&nbsp;       ├── movies.csv

&nbsp;       ├── people.csv

&nbsp;       └── stars.csv

▶️ Run

Bash



cd search-algorithms/bfs-actor-connections



\# Using small dataset (fast)

python degrees.py data/small



\# Using large dataset (full IMDb)

python degrees.py data/large

📸 Sample Output

text



$ python degrees.py data/large

Loading data...

Data loaded.

Name: Emma Watson

Name: Tom Hanks

3 degrees of separation.

1: Emma Watson and Brendan Gleeson starred in Harry Potter and the Goblet of Fire

2: Brendan Gleeson and Tom Hanks starred in The Green Mile

2\. Minimax Tic-Tac-Toe

Unbeatable AI — Optimal game-playing agent using Minimax algorithm with perfect play.



<table> <tr> <td width="50%">

📝 Problem Statement

Build an AI that plays Tic-Tac-Toe optimally. The AI should:



Never lose

Win whenever possible

Force draw against perfect opponent

</td> <td width="50%">

📊 Complexity Analysis

Metric	Value

Algorithm	Minimax

Time	O(b^d) ≈ O(9!)

Space	O(d) = O(9)

Optimality	✅ Perfect play

Max States	362,880

</td> </tr> </table>

🔍 How Minimax Works

text



Current State: X's turn (Maximizing)



&nbsp;                        ┌─────────────┐

&nbsp;                        │  X │   │ O  │

&nbsp;                        │────┼───┼────│

&nbsp;                        │    │ X │    │  ← Current board

&nbsp;                        │────┼───┼────│

&nbsp;                        │  O │   │    │

&nbsp;                        └──────┬──────┘

&nbsp;                               │

&nbsp;        ┌──────────────────────┼──────────────────────┐

&nbsp;        ▼                      ▼                      ▼

&nbsp;  ┌───────────┐         ┌───────────┐         ┌───────────┐

&nbsp;  │ X │ X │ O │         │ X │   │ O │         │ X │   │ O │

&nbsp;  │───┼───┼───│         │───┼───┼───│         │───┼───┼───│

&nbsp;  │   │ X │   │         │ X │ X │   │         │   │ X │   │

&nbsp;  │───┼───┼───│         │───┼───┼───│         │───┼───┼───│

&nbsp;  │ O │   │   │         │ O │   │   │         │ O │ X │   │

&nbsp;  └─────┬─────┘         └─────┬─────┘         └─────┬─────┘

&nbsp;        │                     │                     │

&nbsp;   Score: +1             Score: 0              Score: +1

&nbsp;   (X wins)              (Draw)                (X wins)

&nbsp;        

&nbsp;        └──────────────────┬──────────────────┘

&nbsp;                           ▼

&nbsp;                    MAX chooses +1

&nbsp;                   (Best move: win)

🎮 Game Theory Concepts

text



┌────────────────────────────────────────────────────────────┐

│                     MINIMAX PRINCIPLE                       │

├────────────────────────────────────────────────────────────┤

│                                                            │

│   MAX Player (X): Wants to MAXIMIZE score                  │

│   MIN Player (O): Wants to MINIMIZE score                  │

│                                                            │

│   Utility Values:                                          │

│   ┌─────────┬─────────┬─────────┐                         │

│   │ X Wins  │  Draw   │ O Wins  │                         │

│   │   +1    │    0    │   -1    │                         │

│   └─────────┴─────────┴─────────┘                         │

│                                                            │

│   Strategy: Assume opponent plays optimally               │

│                                                            │

└────────────────────────────────────────────────────────────┘

💻 Implementation

Python



def minimax(board):

&nbsp;   """

&nbsp;   Returns the optimal action for the current player on the board.

&nbsp;   

&nbsp;   Uses recursive minimax to evaluate all possible game states

&nbsp;   and choose the move that leads to the best guaranteed outcome.

&nbsp;   """

&nbsp;   if terminal(board):

&nbsp;       return None

&nbsp;   

&nbsp;   current\_player = player(board)

&nbsp;   

&nbsp;   if current\_player == X:

&nbsp;       # Maximizing player

&nbsp;       best\_value = float('-inf')

&nbsp;       best\_action = None

&nbsp;       

&nbsp;       for action in actions(board):

&nbsp;           value = min\_value(result(board, action))

&nbsp;           if value > best\_value:

&nbsp;               best\_value = value

&nbsp;               best\_action = action

&nbsp;               

&nbsp;       return best\_action

&nbsp;   

&nbsp;   else:

&nbsp;       # Minimizing player

&nbsp;       best\_value = float('inf')

&nbsp;       best\_action = None

&nbsp;       

&nbsp;       for action in actions(board):

&nbsp;           value = max\_value(result(board, action))

&nbsp;           if value < best\_value:

&nbsp;               best\_value = value

&nbsp;               best\_action = action

&nbsp;               

&nbsp;       return best\_action





def max\_value(board):

&nbsp;   """Returns maximum value for maximizing player."""

&nbsp;   if terminal(board):

&nbsp;       return utility(board)

&nbsp;   

&nbsp;   v = float('-inf')

&nbsp;   for action in actions(board):

&nbsp;       v = max(v, min\_value(result(board, action)))

&nbsp;   return v





def min\_value(board):

&nbsp;   """Returns minimum value for minimizing player."""

&nbsp;   if terminal(board):

&nbsp;       return utility(board)

&nbsp;   

&nbsp;   v = float('inf')

&nbsp;   for action in actions(board):

&nbsp;       v = min(v, max\_value(result(board, action)))

&nbsp;   return v

📁 Project Structure

text



adversarial-search/minimax-tictactoe/

├── tictactoe.py        # Game logic + Minimax AI

└── runner.py           # Pygame graphical interface

▶️ Run

Bash



cd adversarial-search/minimax-tictactoe



\# Install dependency

pip install pygame



\# Run the game

python runner.py

🎮 Game Features

Feature	Description

Play as X or O	Choose your side

AI Never Loses	Optimal play guaranteed

Visual Interface	Clean Pygame GUI

Move Highlighting	See AI's decision

📸 Demos

BFS Actor Connections

text



┌────────────────────────────────────────────────────────────┐

│  $ python degrees.py data/large                            │

│                                                            │

│  Loading data...                                           │

│  Data loaded.                                              │

│  Name: Emma Watson                                         │

│  Name: Johnny Depp                                         │

│                                                            │

│  2 degrees of separation.                                  │

│  1: Emma Watson and Helena Bonham Carter starred in        │

│     Harry Potter and the Order of the Phoenix              │

│  2: Helena Bonham Carter and Johnny Depp starred in        │

│     Sweeney Todd: The Demon Barber of Fleet Street         │

│                                                            │

└────────────────────────────────────────────────────────────┘

Minimax Tic-Tac-Toe

text



┌─────────────────────────────────────┐

│         TIC-TAC-TOE AI              │

│                                     │

│    ┌─────┬─────┬─────┐             │

│    │  X  │  O  │  X  │             │

│    ├─────┼─────┼─────┤             │

│    │     │  X  │     │             │

│    ├─────┼─────┼─────┤             │

│    │  O  │     │  O  │             │

│    └─────┴─────┴─────┘             │

│                                     │

│    AI is thinking...                │

│    AI plays: (2, 1)                 │

│                                     │

└─────────────────────────────────────┘

🏗️ Architecture

text



Classical-ai-implementations/

│

├── 📁 search-algorithms/

│   │

│   └── 📁 bfs-actor-connections/

│       ├── 📄 degrees.py           # BFS implementation

│       ├── 📄 util.py              # Data structures

│       └── 📁 data/

│           ├── 📁 small/           # Test dataset

│           └── 📁 large/           # Production dataset

│

├── 📁 adversarial-search/

│   │

│   └── 📁 minimax-tictactoe/

│       ├── 📄 tictactoe.py         # Game logic + AI

│       └── 📄 runner.py            # GUI interface

│

├── 📄 README.md

├── 📄 LICENSE

├── 📄 requirements.txt

└── 📄 .gitignore

🔬 Algorithms Deep Dive

Search Algorithms Comparison

Algorithm	Completeness	Optimality	Time	Space	Use Case

BFS	✅	✅ (unweighted)	O(b^d)	O(b^d)	Shortest path

DFS	❌	❌	O(b^m)	O(bm)	Memory limited

A\*	✅	✅	O(b^d)	O(b^d)	Informed search

Greedy	❌	❌	O(b^m)	O(b^m)	Fast approximation

Game Theory Algorithms

Algorithm	Description	Optimality	Pruning

Minimax	Full game tree search	✅ Perfect	❌

Alpha-Beta	Minimax with pruning	✅ Perfect	✅

Expectimax	Handles randomness	Optimal in expectation	❌

🔮 Upcoming Projects

<table> <tr> <td width="33%">

🎮 Minesweeper AI

Algorithm: Propositional Logic



text



Knowledge-Based Agent:

• Logical sentences

• Inference rules  

• Safe cell deduction

• Mine identification

Status: 🔄 In Progress



</td> <td width="33%">

📊 PageRank

Algorithm: Markov Chains



text



Probabilistic Model:

• Random surfer model

• Stationary distribution

• Iterative computation

• Damping factor

Status: 📅 Planned



</td> <td width="33%">

🧬 Heredity

Algorithm: Bayesian Networks



text



Probabilistic Inference:

• Gene inheritance

• Conditional probability

• Joint distribution

• Family tree modeling

Status: 📅 Planned



</td> </tr> <tr> <td width="33%">

📝 Crossword Solver

Algorithm: CSP + AC-3



text



Constraint Satisfaction:

• Variable assignment

• Domain reduction

• Arc consistency

• Backtracking search

Status: 📅 Planned



</td> <td width="33%">

🗣️ Parser

Algorithm: Context-Free Grammar



text



Natural Language:

• Sentence parsing

• Syntax trees

• Noun phrase extraction

• Grammar rules

Status: 📅 Planned



</td> <td width="33%">

✍️ Attention Model

Algorithm: Transformers



text



Deep Learning:

• Self-attention

• Masked language model

• Text prediction

• Neural networks

Status: 📅 Planned



</td> </tr> </table>

🛠️ Tech Stack

<table> <tr> <td align="center" width="20%"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" width="48" height="48" alt="Python" /> <br><strong>Python 3.10+</strong> <br><sub>Core Language</sub> </td> <td align="center" width="20%"> <img src="https://www.pygame.org/docs/\_static/pygame\_tiny.png" width="48" height="48" alt="Pygame" /> <br><strong>Pygame</strong> <br><sub>Game GUI</sub> </td> <td align="center" width="20%"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/git/git-original.svg" width="48" height="48" alt="Git" /> <br><strong>Git</strong> <br><sub>Version Control</sub> </td> </tr> </table>

Core Concepts

text



┌─────────────────────────────────────────────────────────────┐

│                    KNOWLEDGE AREAS                          │

├──────────────────┬──────────────────┬───────────────────────┤

│   Data Structures│    Algorithms    │      AI Concepts      │

├──────────────────┼──────────────────┼───────────────────────┤

│ • Queues         │ • BFS/DFS        │ • State Space Search  │

│ • Stacks         │ • Minimax        │ • Game Trees          │

│ • Hash Maps      │ • Alpha-Beta     │ • Heuristics          │

│ • Graphs         │ • Backtracking   │ • Utility Functions   │

│ • Trees          │ • Recursion      │ • Adversarial Search  │

└──────────────────┴──────────────────┴───────────────────────┘

⚡ Quick Start

Prerequisites

Python 3.10 or higher

pip package manager

Git

Installation

Bash



\# Clone the repository

git clone https://github.com/vickysharma-prog/Classical-ai-implementations-.git



\# Navigate to project directory

cd Classical-ai-implementations-



\# Install dependencies

pip install -r requirements.txt

Run Projects

Bash



\# Project 1: BFS Actor Connections

cd search-algorithms/bfs-actor-connections

python degrees.py data/small



\# Project 2: Minimax Tic-Tac-Toe

cd adversarial-search/minimax-tictactoe

python runner.py

🤝 Contributing

Contributions are welcome! Here's how you can help:



Fork the repository

Create a feature branch (git checkout -b feature/amazing-feature)

Commit changes (git commit -m 'Add amazing feature')

Push to branch (git push origin feature/amazing-feature)

Open a Pull Request

Contribution Ideas

&nbsp;Add Alpha-Beta pruning to Minimax

&nbsp;Implement A\* search algorithm

&nbsp;Add unit tests

&nbsp;Create interactive visualizations

&nbsp;Add more datasets

📚 References

Book: Russell, S., \& Norvig, P. Artificial Intelligence: A Modern Approach (4th Edition)

Course: Harvard CS50's Introduction to AI with Python

Documentation: Python Official Docs

📄 License

text



MIT License



Copyright (c) 2024 Vicky Sharma



Permission is hereby granted, free of charge, to any person obtaining a copy

of this software and associated documentation files (the "Software"), to deal

in the Software without restriction, including without limitation the rights

to use, copy, modify, merge, publish, distribute, sublicense, and/or sell

copies of the Software, and to permit persons to whom the Software is

furnished to do so, subject to the following conditions:



The above copyright notice and this permission notice shall be included in all

copies or substantial portions of the Software.



THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR

IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,

FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE

AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER

LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,

OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE

SOFTWARE.

👤 Author

<table> <tr> <td align="center"> <strong>Vicky Sharma</strong> <br> <a href="https://github.com/vickysharma-prog"> <img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge\&logo=github\&logoColor=white" /> </a> </td> </tr> </table>

<div align="center">

⭐ Star this repository if you found it helpful!

Made with ❤️ and Python



</div> ```

