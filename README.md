TypeSprint - Python Typing Speed Test

TypeSprint is a desktop typing practice application built with Python and Tkinter. The user types a randomly selected passage while a 30-second timer runs. The app highlights matching and incorrect characters, displays live words per minute (WPM) and accuracy, and presents a final result.

## Features

- Random English passage for each round
- Timer starts automatically on the first keystroke
- Live character-by-character feedback
- Live WPM and accuracy calculations
- Completion or timeout result dialog with a performance rating
- **New Test** button to restart with a different passage

## Requirements

- Python 3.8 or newer
- Tkinter (usually included with the standard Python installation)

The project uses only Python standard-library modules; no `pip install` step is required.

## Run locally

1. Download or clone this repository.
2. Open a terminal in the folder containing `typing_test.py`.
3. Run:

   ```bash
   python typing_test.py
   ```

   On some systems, use `python3 typing_test.py`.
4. Type in the input box to start the timer. Click **New Test** to play another round.

If Tkinter is unavailable, install the Tk GUI support package for your Python distribution, then run the command again.

## How it works

1. The app chooses one sentence from the built-in `PASSAGES` list.
2. The first typed character stores the start time and schedules timer updates through Tkinter's event loop.
3. After each keystroke, the typed text is compared with the target passage. Matching characters are shown in green; mismatches are shown in red.
4. The app recalculates the live WPM and accuracy values.
5. The round ends when the passage is completed or 30 seconds elapse. The app displays the final score and rating.

## Scoring

- **WPM** = number of whitespace-separated words typed / elapsed time in minutes.
- **Accuracy** = correctly matched typed characters / total typed characters x 100.
- A typed character is considered correct when it matches the target character at the same position.

This is a simple educational scoring model. It does not apply a standard five-character word convention or subtract errors from WPM.

## Project structure

```text
typing_test.py                 # Application source code
README.md                      # Setup, usage, and project notes
typesprint_project_report.pdf  # Academic project report
typing_speed_test_python.pdf   # Source-code handout
```

## Approach and findings

The program is organized in a `TypingSpeedTest` class. Tkinter handles the interface and event loop; `time` measures the elapsed test duration; `random` selects passages. Keeping timer updates in Tkinter's `after()` event loop lets the window remain responsive while the countdown runs.

During development, a key behavior is that the timer should begin only after the user starts typing, so the user can read the passage first. Character-level comparison provides immediate feedback, while the final dialog summarizes the result. The current implementation is intentionally lightweight and does not save personal scores between runs.

## Testing checklist

- Start the app and confirm the passage and idle timer are visible.
- Type a character and confirm the countdown begins.
- Type matching and mismatching characters and check the color feedback.
- Complete the passage and confirm the result dialog appears.
- Start another round and confirm the passage and timer reset.
- Leave a round running until timeout and confirm input is disabled and results appear.

## Limitations and future work

- Scores are not saved after the application closes.
- Passage collection is fixed and English-only.
- Current WPM uses typed words, including words with mistakes.
- Future versions could add persistent score history, adjustable duration, difficulty levels, more languages, and score charts.

## Documentation

See [`typesprint_project_report.pdf`](typesprint_project_report.pdf) for the project report and [`typing_speed_test_python.pdf`](typing_speed_test_python.pdf) for a printable source-code handout.
