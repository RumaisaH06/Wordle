# Wordle
A hardware-based implementation of the [***New York Times' Wordle***](https://www.nytimes.com/games/wordle/index.html), written ***entirely in Verilog*** and deployed on the FGPA of the ***Altera DE1-SoC development board***.

## Overview
A recreation of the iconic Wordle game, implemented as a **fully hardware-based system**. The objective is to **guess a hidden five-letter word within six attempts**. After each guess, **letters receive colour-coded feedback** indicating whether they are correctly placed, misplaced, or not present in the target word. 


## Key Features
- **Five-letter word guess** requirement, **six attempts** per game
- **Colour-coded feedback** for correct, misplaced, and incorrect letters
    - **Green:** Correct letter and position
    - **Yellow:** Correct letter, incorrect position
    - **Grey:** Letter not in word
- **Win/loss detection**
- **PS/2 keyboard input** with valid-key filtering
- **Finite State Machines (FSMs)** for game flow and control logic
- **VGA-based graphics** with 640x480 resolution, 9-bit colour, and real-time display of the grid, tiles, and letters using sprite sheets and hardware logic.
- **LED & HEX displays** for supplementary input tracking and letter evaluation

## Hardware Requirements
- Altera DE1-SoC development board
- PS/2 Keyboard
- VGA monitor

  
## Game Controls
| Input | Action |
|-------|----------|
| A–Z | Enter a letter |
| Backspace | Delete last letter |
| Enter | Submit a guess |
| KEY[0] | Reset Game (active-low) |


## File Structure
### Core Modles
| Module | Responsibility |
|---|---|
| `wordleTopLevel.v` | Integrates the main game components |
| `eventParser.v` | Converts PS/2 scancodes into usable game actions |
| `buffers.v` | Stores guesses and target word data |
| `compareWord.v` | Compares guesses with the target word and determines letter feedback encoding |
| `FSM.v` | Controls game flow and state transitions |
| `wordleDisplay.v` | Manages VGA game display |
| `drawTileColor.v` | Draws coloured background tiles (green, yellow, grey) |
| `drawLetter.v` | Renders 38×37-pixel letters onto the VGA display using bitmap data from the sprite ROM |
| `sprite_sheet.v` | Stores letter bitmap data |

### Support Modules

- `PS2_Controller.v` — PS/2 keyboard interface
- `vga_adapter.v` — VGA display interface (Altera UP IP)


## Demo & Documentation
You can **play this hardware implementation of Wordle** on a DE1-SoC board **using the pre-compiled .sof bitstream included in this repository** — no compiling required!

For a [**video demonstration**](https://drive.google.com/file/d/1SIdMMECNzBhE1qUAftU6ibAehWEAVIoi/view?usp=sharing) and a more detailed look at how the project works, including its key modules, take a look at the [**project walkthrough**](https://docs.google.com/presentation/d/1X9SdHf20ZQwOY385aegQYKhJjI_BFVfq20xbA3PbWWQ/edit?usp=sharing).

<p align="center">
  <img width="456" height="78" alt="WORDLE" src="https://github.com/user-attachments/assets/25c4c346-7f34-4d6e-92a6-4545c2e0d87b" />
</p>
