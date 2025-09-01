# Benkyou - Japanese Language Learning App

## Project Overview
Benkyou is a local Japanese language learning application built with Python and PyQt6, designed to help users learn Japanese vocabulary through spaced repetition. The app follows a similar style to Anki, focusing on active recall and long-term retention.

## Core Goals
1. **Language Learning App**: Create a local Python application similar to Anki for Japanese vocabulary study
2. **Spaced Repetition**: Implement spaced repetition algorithms to optimize learning retention
3. **Typing-Based Learning**: Users type answers in Romanji, with real-time conversion to hiragana/katakana
4. **Bidirectional Learning**: Support English→Japanese, Japanese→English, and mixed quiz modes
5. **Progress Persistence**: Save and load user progress across app sessions
6. **Deck Management**: Support multiple vocabulary decks with independent progress tracking

## Technical Stack
- **Language**: Python 3.13+
- **GUI Framework**: PyQt6 (≥6.9.1)
- **Package Manager**: UV
- **Dependencies**: See `pyproject.toml` for current dependencies
- **Architecture**: Object-oriented with modular design

## Project Structure
```
benkyou/
├── main.py                          # Application entry point
├── spaced_repetition/              # Core spaced repetition logic
│   ├── __init__.py
│   └── card.py                     # Card class with SM-2 algorithm
├── vocab_files/                    # Vocabulary deck storage
│   └── N5.csv                      # JLPT N5 vocabulary deck
├── pyproject.toml                  # Project configuration
└── README.md                       # Project documentation
```

## Core Features

### 1. Spaced Repetition System
The app implements a sophisticated spaced repetition algorithm via the `Card` class:

- **Learning Phase**: Cards start in "learning" status with graduated intervals (1min → 6min → 10min → 1day → 4days)
- **Review Phase**: Cards enter "reviewing" status with dynamic intervals based on ease factor
- **Relearning**: Failed cards return to "relearning" with adjusted intervals
- **Ease Factor**: Adaptive difficulty adjustment (1.3 minimum, increases with success)

### 2. Vocabulary Management
- **Deck System**: Multiple vocabulary decks stored in `./vocab_files/`
- **CSV Format**: Decks use CSV format with columns: [Japanese, Reading, English]
- **Progress Tracking**: Independent progress tracking per deck
- **Deck Selection**: Users choose which deck to study on app launch

### 3. Quiz Modes
- **English → Japanese**: Given English word, type Japanese in Romanji
- **Japanese → English**: Given Japanese word, type English meaning
- **Mixed Mode**: Random selection between the two modes for each card

### 4. Real-Time Input Conversion
- **Romanji Input**: Users type using standard Romanji (e.g., "benkyoushimasu") on English keyboard
- **Dynamic Conversion**: Real-time conversion to hiragana/katakana as user types
- **Script Detection**: Automatic detection of appropriate script (hiragana/katakana -> lower-case/upper-case)
- **Usage Context**: Conversion only occurs when translating from English to Japanese (English→Japanese mode)
- **Script Convention**: Katakana for uppercase, hiragana for lowercase

## Implementation Guidelines

### 1. Core Architecture
- **Main Window**: PyQt6-based main application window
- **Card Manager**: Handles card presentation and user interaction
- **Progress Manager**: Manages user progress persistence
- **Deck Manager**: Handles vocabulary deck loading and selection

### 2. Data Flow
```
User Input → Romanji Processing → Kana Conversion (English→Japanese only) → Answer Validation → Spaced Repetition Update → Progress Save
```

### 3. Progress Persistence
- **Format**: JSON-based progress files
- **Location**: User-specific progress directory
- **Structure**: Per-deck progress with card status, intervals, and ease factors
- **Auto-save**: Progress saved after each card interaction

### 4. User Interface Requirements
- **Clean Design**: Modern, intuitive interface similar to Anki or Quizlet
- **Smooth Experience**: Optimized for fluid, responsive interactions with minimal lag
- **Typing Interface**: Dedicated typing area for user input with real-time feedback
- **Answer Validation**: Clear indication of correct/incorrect answers with corrections
- **Responsive Layout**: Adapts to different screen sizes
- **Keyboard Navigation**: Full keyboard support for efficient study
- **Progress Indicators**: Visual feedback on study progress and statistics

## Development Guidelines

### 1. Code Standards
- **Python 3.13+**: Use modern Python features and type hints
- **PEP 8**: Follow Python style guidelines
- **Documentation**: Comprehensive docstrings for all classes and methods
- **Type hints**: Every function should have type hints and if necessary a docstring
- **Error Handling**: Robust error handling with user-friendly messages

### 2. Performance Considerations
- **Efficient Algorithms**: Optimize spaced repetition calculations
- **Memory Management**: Handle large vocabulary decks efficiently
- **UI Responsiveness**: Ensure smooth user experience during typing and conversion

## Future Enhancements (Consider for Implementation)
- **Audio Support**: Pronunciation audio for vocabulary words
- **Statistics Dashboard**: Detailed learning analytics and progress charts
- **Custom Decks**: User-created vocabulary decks
- **Export/Import**: Progress backup and sharing functionality
- **Mobile Support**: Responsive design for tablet/phone use
- **Grammar Integration**: Basic grammar explanations and exercises

*Note: These features are not currently planned for the initial implementation but may be added in future versions.*

## Dependencies and Libraries
**Current Dependencies:**
- PyQt6 ≥6.9.1 (GUI framework)
- romkan (Romaji to Kana conversion) <- sourcecode from https://github.com/soimort
- simple-spaced-repetition <- sourcecode from https://github.com/vlopezferrando/simple-spaced-repetition

## Getting Started
1. Ensure Python 3.13+ is installed
2. Install UV package manager
3. Clone the repository
4. Run `uv sync` to install dependencies
5. Execute `python main.py` to start the application

## Building an Executable

### Prerequisites
- UV package manager installed


#### Option: Shell Script (Linux/macOS/WSL)
```bash
# Run the shell script
./build.sh
```

### What the Build Scripts Do
1. **Clean Previous Builds**: Remove old `dist/` and `build/` directories
2. **Install Dependencies**: Add PyInstaller as a dev dependency and sync all packages
3. **Create Configuration**: Generate a PyInstaller spec file optimized for your PyQt6 app
4. **Bundle Application**: Create a standalone executable with all dependencies included
5. **Include Data Files**: Automatically bundle your `vocab_files/` and `progress_files/` directories

### Output
- **Windows**: `dist/benkyou.exe` - Standalone Windows executable
- **Linux/macOS**: `dist/benkyou` - Native executable for the target platform
- **Type**: Standalone executable (no Python installation required)
- **Size**: Typically 50-100MB depending on dependencies
- **Distribution**: Can be shared with users on the same platform

### Troubleshooting
- **UV not found**: Install UV from https://docs.astral.sh/uv/getting-started/installation/
- **Build fails**: Check that you're running the script from the project root directory
- **Missing dependencies**: The script automatically installs PyInstaller and syncs dependencies


# Contributing
Make a PR. I'll get an email and review it ASAP.
