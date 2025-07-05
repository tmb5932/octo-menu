# Chip8 ROM Game Selection Menu
This project will hopefully eventually contain a ROM for a Chip8 emulator that allows for selecting a game to be played. This will obviously require support from the outside language, as the Chip8 emulator has no capabilities to load files or similar on its own.

## The Goal
I want to create a menu in entirely Octo (Chip8 assembly language), that can display a list of games to be played, allow the user to scroll through it, and make a selection.

The list of games to be displayed as options would be preemtively loaded into memory somewhere as a list of names, and once a game is selected, the selected games ID (the position in the passed in array) would be available in the V0 register, that the outside program could then read and load said game into the emulator.

## Most current version
Currently, I have a menu that can scroll between the letters of the alphabet, and return the ID (the location in passed in list) of the selected letter.

https://johnearnest.github.io/Octo/index.html?key=U8KKlnJ0

### Next Iterations Improvements:
- Read the values in from the Chip8's memory, instead of having them preemptively in the data 

## Requirements
The only requirements to do this is to have a list of the games to be options, and to have the ability to have the rom close the emulator. Although a bit abnormal, especially for emulators, giving support for returning from the main function in the ROM is a good way to do this.

A quick example (in psuedo code), would see it as something like this

```
// In decode/execute part of emulator code
if instruction = RETURN_FROM_SUB_FUNCTION:

    // If trying to return from main (close emulator)
    if self.stack_pointer == 0:
        // Return a value that the code checks for, and if it is a special value
        //  like EXIT_ROM, it breaks the loop.
        return EXIT_ROM;

    // Normal use of this command
    self.stack_pointer -= 1;              
    self.program_counter = self.stack[self.stack_pointer];
...

// In the main loop of the emulator
return_value = emulator.cycle();
if return_value == EXIT_ROM:
    break loop
...
```

## Limitations
The main limitation at this point is max number of games able to be loaded into the rom to be chosen from.
This is just a speculative cap at this point, but it is definitely hard capped at 256 (num of different values of a u8, which is what the registers are). This isn't that big of a deal, as hopefully there aren't more than 256 games in the library.

## Notes
I know this would have been simpler to do entirely in a programming language, but I created a Chip8 emulator and thought it would be cool to make my own ROM. So, instead of creating another Snake ROM, which I'm sure dozens of others if not more have done, I made this.


## Author
Travis Brown (tmb5932)
