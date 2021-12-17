# Playing Guitar
### Question
Kimcoding has a new imaginary extraterrestrial friend with a billion of fingers.
The extraterrestrial has soon took hold of his guitar, found a simple melody online, and started playing it.

The guitar, as usual, has six strings denoted by numbers 1 through 6. Each string is divided into P frets denoted by numbers 1 through P.
A melody is a sequence of tones, where each tone is produced by picking a string pressed on a specific fret (e.g. 4th string pressed on the 8th fret).
If a string is pressed on several frets, the produced tone will be the one corresponding to the highest of those frets.

For instance, if the 3rd string is already pressed on the 5th fret, and the tone which corresponds to the 7th fret is to be produced,
the string can be pressed on the 7th fret and picked without releasing the 5th fret, since only the highest one affects the tone produced (7th in this case).

Similarly, if a tone that corresponds to the 2nd fret on the same string is next to be produced, it is necessary to release both 5th and 7th frets.
Write a program which computes the minimum number of finger movements needed to produce the given melody.

Note that press or release a single fret counts as one finger move. String picking does not count as finger move, but rather a guitar pick move.

### Input
Parameter 1: playingArr
The first array of input contains two positive integers separated by a single space, N (N ≤ 500 000) and P (2 ≤ P ≤ 300 000).

They represent the number of tones in the melody and the number of frets, respectively.

The following N arrays describe the fields for the corresponding tones – the ordinal of the string and the ordinal of the fret, respectively, in the same order as the extraterrestrial play them.
### Output
In a single line of output, print the minimum number of finger movements.
### I/O Example
```js
let playingArr = [["5","15"],["3","8"],["3","9"],["3","6"],["3","4"],["2","7"]]

let output = countOfFingerMVs(playingArr);
console.log(output); // 8

playingArr = [["6","15"],["2","8"],["3","9"],["3","6"],["2","4"],["2","1"],["2","3"]]

output = countOfFingerMVs(playingArr);
console.log(output); // 9
```

- - -
### SOLUTION
```js
function countOfFingerMVs(playingArr){
  const [numberOfMelodies, totalFret] = playingArr[0].map(Number);
  const lines = Array(7).fill().map(el => []);
   let count = 0;
   for(let i = 1; i <= numberOfMelodies; i++){
     const [line, fret] = playingArr[i].map(Number);
     const lineStack = lines[line];

      while(lineStack.length){
       if (lineStack[lineStack.length - 1] > fret){
        lineStack.pop();
        count++;
      }else if(lineStack[lineStack.length - 1] === fret){
        lineStack.pop();
        count--;
        break;
      }else{
        break;
      }
    }
    lineStack.push(fret);
    count++;
  
  }
  return count
}
```
