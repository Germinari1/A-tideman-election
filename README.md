# Tideman Election Algorithm

This program implements the Tideman election algorithm, which is a ranked-pair voting system that ensures the existence of a source (a candidate who is preferred over all other candidates) in the graph of preferences. The algorithm takes input from voters ranking the candidates and determines the winner of the election based on the voters' preferences.

## Usage

To run the program, compile and execute the source code file. The program will prompt you to enter the number of voters and their preferences for the candidates. The candidates should be provided as command-line arguments when running the program:
```txt
./tideman [candidate1] [candidate2] ... [candidateN]
```
Replace `[candidate1]`, `[candidate2]`, ..., `[candidateN]` with the names of the candidates in the election.

## Algorithm Overview

1. The program prompts the user to enter the number of voters and their preferences for the candidates.
2. For each voter, the program records their preferences by updating the `preferences` array, which keeps track of the number of voters who prefer one candidate over another.
3. The `add_pairs` function is called to create an array of pairs of candidates, where one candidate is preferred over the other. The pairs are ordered based on the strength of the victory (the difference in the number of voters who prefer one candidate over the other).
4. The `sort_pairs` function sorts the pairs in decreasing order by the strength of victory using bubble sort.
5. The `lock_pairs` function locks in the pairs of candidates into the `locked` array (representing the graph of preferences) without creating cycles. This is done by using a recursive helper function `cycle_checker` to check if adding a new edge (locking a pair) would create a cycle in the graph.
6. The `print_winner` function prints the winner of the election by finding the candidate who is not pointed to by any other candidate in the `locked` array (the source of the graph).

## Implementation Details

The program uses the following data structures and functions:

- `preferences[MAX][MAX]`: A 2D array that stores the number of voters who prefer one candidate over another.
- `locked[MAX][MAX]`: A 2D array that represents the graph of preferences, where `locked[i][j]` means that candidate `i` is locked in over candidate `j`.
- `candidates[MAX]`: An array that stores the names of the candidates.
- `pairs[MAX * (MAX - 1) / 2]`: An array that stores the pairs of candidates, where one candidate is preferred over the other.
- `vote(int rank, string name, int ranks[])`: Updates the `ranks` array with the voter's preference for a given candidate.
- `record_preferences(int ranks[])`: Updates the `preferences` array based on the voter's preferences.
- `add_pairs()`: Creates the array of pairs of candidates, where one candidate is preferred over the other.
- `sort_pairs()`: Sorts the pairs in decreasing order by the strength of victory using bubble sort.
- `cycle_checker(int cand_winner, int cand_loser)`: A recursive helper function that checks if adding a new edge (locking a pair) would create a cycle in the graph of preferences.
- `lock_pairs()`: Locks in the pairs of candidates into the `locked` array without creating cycles, using the `cycle_checker` function.
- `print_winner()`: Prints the winner of the election by finding the candidate who is not pointed to by any other candidate in the `locked` array.

## Example

Suppose we have 5 candidates (Alice, Bob, Charlie, David, and Emma) and 3 voters with the following preferences:

Voter 1: Alice > Bob > Charlie > David > Emma
Voter 2: Emma > David > Charlie > Bob > Alice
Voter 3: Charlie > Alice > Emma > Bob > David

Running the program with the command:
```txt
./tideman Alice Bob Charlie David Emma
```
The program will prompt for the number of voters and their preferences. After entering the preferences, the program will output the winner of the election based on the Tideman algorithm.
