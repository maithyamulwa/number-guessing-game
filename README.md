# Number Guessing Game

A command-line number guessing game written in Python. It was built as a beginner-friendly project to practice **conditional statements** (`if` / `elif` / `else`), **functions**, **loops**, and **input validation**.

## Features

- Three difficulty levels with different ranges and attempt limits
- Hints after every guess ("Too low" or "Too high")
- Score out of 100 based on how few attempts you used
- Play multiple rounds and track your wins
- Rejects non-numeric and out-of-range guesses without using up an attempt
- Built-in tests that need no extra libraries

## Difficulty Levels

| Level | Range | Attempts |
|---|---|---|
| Easy | 1 - 50 | 10 |
| Medium | 1 - 100 | 7 |
| Hard | 1 - 200 | 6 |

## Requirements

- Python 3.6 or newer (uses f-strings)
- No third-party packages

## Getting Started

Clone the repository and run the game:

```bash
git clone https://github.com/<your-username>/number-guessing-game.git
cd number-guessing-game
python number_guessing_game.py
```

## Usage

Pick a difficulty, then guess until you find the number or run out of attempts:

```
Welcome to the Number Guessing Game!

Choose difficulty:
  1) Easy: number between 1 and 50, 10 attempts
  2) Medium: number between 1 and 100, 7 attempts
  3) Hard: number between 1 and 200, 6 attempts
Your choice: 1

I am thinking of a number between 1 and 50.

Guess (10 attempts left): 25
Too high.

Guess (9 attempts left): 10
Too low.

Guess (8 attempts left): abc
Please enter a whole number.

Guess (8 attempts left): 99
Your guess must be between 1 and 50.

Guess (8 attempts left): 17
Too low.

Guess (7 attempts left): 20
Correct! You got it in 4 attempt(s).
Score: 70/100

Play again? (y/n): n

You won 1 of 1 game(s). Thanks for playing!
```

Invalid guesses ("abc" and 99 above) are rejected and do not count as attempts.

## Scoring

The score is calculated as:

```
score = 100 * (max_attempts - attempts_used + 1) / max_attempts
```

Winning on the first guess always gives 100. Winning on the last allowed attempt gives the lowest passing score for that level (for example, 10 on Easy).

## Using the functions in your own code

```python
from number_guessing_game import check_guess, is_valid_guess, calculate_score

print(check_guess(10, 50))        # Too low
print(check_guess(90, 50))        # Too high
print(check_guess(50, 50))        # Correct
print(is_valid_guess(101, 1, 100))  # False
print(calculate_score(3, 7))      # 71
```

## Running the Tests

```bash
python number_guessing_game.py --test
```

Expected output:

```
PASS  test_check_guess
PASS  test_is_valid_guess
PASS  test_calculate_score
PASS  test_play_round_win
PASS  test_play_round_loss
PASS  test_invalid_input_does_not_use_attempts
PASS  test_choose_difficulty

7/7 tests passed
```

The test functions follow the `test_` naming convention, so they also work with pytest:

```bash
pip install pytest
pytest number_guessing_game.py
```

## Project Structure

```
number-guessing-game/
├── number_guessing_game.py   # Game logic, interactive loop, and tests
└── README.md
```

## How It Works

| Function | Purpose |
|---|---|
| `check_guess(guess, secret)` | Returns "Too low", "Too high", or "Correct" using `if/elif/else` |
| `is_valid_guess(guess, low, high)` | Returns `True` if the guess is inside the allowed range |
| `calculate_score(attempts_used, max_attempts)` | Returns a score from 0 to 100 |
| `choose_difficulty(input_func)` | Asks for a difficulty and returns its settings |
| `play_round(secret, low, high, max_attempts, input_func)` | Runs one round and returns attempts used, or `None` if lost |
| `main()` | Picks the secret number, runs rounds, and tracks wins |

`play_round()` and `choose_difficulty()` take an `input_func` parameter that defaults to the built-in `input`. The tests pass in a fake function that supplies prepared answers, so loops that depend on user input can be tested automatically without typing.

## Strategy Tip

Guessing the middle of the remaining range each time (binary search) halves the possibilities with every guess. This guarantees a win within 6 guesses on Easy and 7 on Medium. Hard needs up to 8 guesses in the worst case but only allows 6, so it takes some luck.

## Concepts Demonstrated

- `if` / `elif` / `else` chains
- Comparison operators and chained comparisons (`low <= guess <= high`)
- Functions with parameters, default values, and `return` values
- `while` loops with `break` and `continue`
- `try` / `except` for input validation
- Dictionaries (the difficulty settings)
- Random numbers with the `random` module
- Testing with `assert` and fake input functions

## Ideas for Extending the Project

- Add a high-score table saved to a file
- Let the player enter their name
- Give "warmer" and "colder" hints based on distance
- Add a custom difficulty with a player-chosen range
- Add a timer for each round
- Rewrite the tests with `unittest` or `pytest`

## License

This project is licensed under the MIT License. Feel free to use it for learning.
