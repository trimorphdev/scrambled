# Scrambled
A NxN Rubik's cube scrambling library for Node.js

```
npm i --save scrambled
```

# Command Line
Scrambled comes packaged with a nifty command line tool:
```sh
scrambled --help
```

## CLI Scramble Generation
```sh
scrambled generate [-s/--size] [-c/--count]
```

This command generates a scramble, with the optional options being:
- `-s/--size`: the size of the Rubik's cube to scramble
- `-c/--count`: the amount of moves the scramble has

## CLI Scramble Verification
```sh
scrambled verify [-s/--scramble] [-t/--token] [-S/--size]
```
Checks if a scramble was generated by Scrambled.

- `-s/--scramble`: **required:** the scramble to check.
- `-t/--token`: **required:** the authentication token provided when the scrambl was generated
- `-S/--size`: **required:** the size of the Rubik's cube to check

# API
## Scrambling
You can scramble a cube using the `scrambled.generateScramble` method:
```js
const scrambled = require('scrambled');

scrambled.generateScramble(30) // Generate scramble with 30 moves
    .then((result) => {
        console.log(result.scramble);
    });
```

## Synchronous Generation
To generate scrambles synchronously, you can use the `scrambled.generateScrambleSync` function.
```js
const scrambled = require('scrambled');

const result = generateScrambleSync(30); // Generate a scramble with 30 moves
console.log(result.scramble);
```

## Arguments
```ts
scramble.generateScramble(count: number, size: number = 3, hash?: string);
```

As you can see, the second argument, `size`, is optional and defaults to a 3x3 Rubik's cube.

If, for example, you want to generate a scramble for a 4x4 Rubik's cube, you can change this argument to 4:
```ts
scramble.generateScramble(30, 4);
```
The first argument is the move count of the scramble, and the second argument is the size of the cube.

The same arguments apply to the `generateScrambleSync` method.

### Seeding
If you want to generate a scramble with your own `seed`, you can provide a 3rd argument, which is a string (keep in mind, you must provide a `size` argument to use a custom seed):
```js
scramble.generateScramble(30, 3, 'my custom seed');
```

## Verification
You can verify if a scramble was generated by Scrambled with the `verifyScramble` and `verifyScrambleSync` methods.

```js
const scrambled = require('scrambled');

const scramble = scramble.generateScrambleSync(30);

scrambled.verifyScramble(scramble.token, scramble.scramble, scramble.size)
    .then((result) => {
        console.log(result); // true or false
    });
```