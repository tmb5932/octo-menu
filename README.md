# Chip8 ROM Selection Menu
This project contains a ROM for a Chip8 emulator that allows for selecting a game to be played. This will obviously require support from the outside language, as the Chip8 emulator has no capabilities to load files or similar on its own.

### Web Tester with Preloaded Example Titles
https://johnearnest.github.io/Octo/index.html?key=qchHNfxa

### Secondary Use
I did not realize this at the start, but this ROM could be used to select anything, from any sort of list. As long as the options are able to be loaded into memory before running the ROM, a selection could be made.

Although if trying to just select from a unchanging list, modifying the basic-A-to-Z.8o menu in the other-menus folder may be better, as no pre-loading of memory needs to be done.

## The Goal
I wanted to create a menu in entirely Octo (Chip8 assembly language), that can display a list of games to be played, allow the user to scroll through it, and make a selection.

The list of games to be displayed as options would be preemtively loaded into memory as a list of names, and once a game is selected, the selected games ID (the position in the passed in array) would be available in the V1 register, that the outside program could then read and load said game into the emulator.

## Most current version
Version has
- Dynamic list of options (Read in from chip8's memory)
- Selected option's ID is left in V1 for access
- Up to 11 characters in each option name
- Takes ASCII characters stored in memory and converts to sprite characters (currently supports ascii characters 32 to 90)
- Wraps. You can't see the top before pressing down again, but going past bottom will put you at top

https://johnearnest.github.io/Octo/index.html?key=qchHNfxa

## Requirements
The only requirements to do this is to have a list of the games to be options to load it in, and to have the ability to have the rom close the emulator. Although a bit abnormal, especially for emulators, giving support for returning from the main function in the ROM is a good way to do this.

**All Titles NEED to be 11 characters long, so pad with spaces if necessary! Also all Titles NEED to be ALL CAPS!**

### Example of Loading in Game Names
To load the game data into the chip8 might look something like this
```
// the actual files names
files = ['snake.ch8', 'pong.ch8', 'battle_ship_shooter_5000.ch8']

// game names EXACTLY 11 CHARACTERS!! any different and it scuffs, so pad with spaces if necessary
titles = ['SNAKE', 'PONG', 'BATTLE STAR']

start_location = 0x500
offset = 0
for title in titles:
    padded = title.left_justify(11, ' ')

    // Add to chip8 memory
    for ch in padded
        let ascii_value = int(ch)
        chip8.memory[start_location + offset as usize] = ascii_value
        offset += 1
```

### Example of Self Closable ROM
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
- Preloading titles

    The obvious limitation is you need to load in the titles of your games in your program, before starting the emulator for this game. 

- Number of titles

    A hard limit at this point is how many name options able to be loaded into the rom in the storage space available. Right now I am using the load point of 0x500, which leaves space for about 230 titles. I might be able to start at 0x4A0 or even early 400's and reach the 256 cap, but for now its ~230.

    The number of options is definitely hard capped at 256 (num of different values of a u8, which is what the registers are). This isn't that big of a deal, as having more than 256 games in the library for a Chip8 device might be excessive.

- Title length

    All the game/option titles need to be exactly 11 characters long. I tested out other ways, such as a delitimeter, but I was unable to figure out a way at the time. Possibly a future improvement.

## Notes
I know this would have been simpler to do entirely in a programming language, but I created a Chip8 emulator and thought it would be cool to make my own ROM. So, instead of creating another Snake ROM, which I'm sure dozens of others if not more have done, I made this.

## Author
Travis Brown (tmb5932)
