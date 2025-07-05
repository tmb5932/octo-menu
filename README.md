# Chip8 ROM Game Selection Menu
This project will hopefully eventually contain a ROM for a Chip8 emulator that allows for selecting a game to be played. This will obviously require support from the outside language, as the Chip8 emulator has no capabilities to load files or similar on its own.

## The Goal
I want to create a menu in entirely Octo (Chip8 assembly language), that can display a list of games to be played, allow the user to scroll through it, and make a selection.
The output would then be stored in a specific place in memory, that the outside program could then read and load said game into the emulator. The list of games to be displayed as options would be preemtively loaded into memory somewhere as a list of names, and the value returned would be the index of the game to load.

## Most current version
Currently, I have a menu that can scroll between the letters of the alphabet, and a cursor to display what is currently being pointed at.
https://johnearnest.github.io/Octo/index.html?key=eIk7415J

### Next Iterations Improvements:
- Save the current letters ID into memory when selected
- Read the values in from the Chip8's memory, instead of having them preemptively in the data 

## Notes
I know this would have been simpler to do entirely in a programming language, but I created a Chip8 emulator and thought it would be cool to make my own rom. So, instead of creating another Snake rom, which I'm sure dozens if not more others have done, I made this.


## Author
Travis Brown (tmb5932)
