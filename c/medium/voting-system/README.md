# Voting System

A small command-line voting program in C. Cast votes for one of four candidates, tally them, and see who's leading.

## What it does

A menu-driven console app with three actions:

1. **Cast the Vote** — pick a candidate (A, B, C, D) or "None of These" (counted as a spoiled vote).
2. **Find Vote Count** — print the running tally for every candidate plus spoiled votes.
3. **Find leading Candidate** — print whoever currently has the most votes.
4. **Exit** (choice `0`).

Votes live in global counters (`votesCount1`–`votesCount4`, `spoiledtvotes`). Nothing is persisted; the tallies reset every run.

This is a practice project — a single-file exercise in menus, `switch`, and a `do/while` loop. No files, no database, no real ballots.

## Build & run

The `makefile.win` in this folder is a Dev-C++ (Windows) file and points at `main.cpp`, but the source here is `main.c`. Easiest path is to compile `main.c` directly:

```sh
gcc main.c -o voting
./voting
```

## Usage example

```
 ##### Welcome to Election/Voting System #####

 1. Cast the Vote
 2. Find Vote Count
 3. Find leading Candidate
 0. Exit

 Please enter your choice : 1

 #### Please Choose your Candidate ####

 1. Candidate A
 2. Candidate B
 3. Candidate C
 4. Candidate D
 5. None of These

 Input Your Choice (1 - 4) : 1
 Thanks for vote !!!!
```

Choose `2` to see the tally, `3` for the current leader.

## Notes on the implementation

- The leading-candidate check uses strict `>` comparisons across all four counts. If the top two candidates are tied (including 0–0 at the start), none of the branches match and it prints `----- Warning !!! No-win situation----`. There's no tie handling.
- The main menu's `default` case prints "Invalid Choice" but the loop continues, so a bad top-level entry just re-shows the menu.
- The cast-vote prompt says "Input Your Choice (1 - 4)" even though option 5 ("None of These") exists.
- `#define CANDIDATE_COUNT` on line 2 is empty and unused.
