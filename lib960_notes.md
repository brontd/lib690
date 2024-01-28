# Class Notes

## Assignment 2.2:  Using Git and GitHub for Documentation

[Git Cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf)

[Rename a file in Git](https://docs.github.com/en/repositories/working-with-files/managing-files/renaming-a-file)

I have some basic familiarity with Git. We use it for library projects here at UK, but I have much to learn. To be honest I feel the same way about Git as I do the remote control to my stereo receiver... so many buttons, but I only use the on/off and volume control... ;-)

## Markdown Experiment with JavaScript

```
// JS code to transform array of arrays into markdown table... run in Chrome Dev Tools, ideally via Sources/Snippets

// Clear console...
clear();

// Array of arrays, with the assumption that the first array corresponds to header fields
let x = [
        ['id', 'make', 'model'],
        ['1', 'Fender', 'Stratocaster'],
        ['2', 'Fender', 'Telecaster'],
        ['2', 'Gibson', 'Les Paul']
    ];

var output = '';

// Iterate array, then sub arrays to create markdown
for(i = 0, xl = x.length; i < xl; i++) {

    output += '| '

    if (i == 0) {

        // Write table header
        for (const v of x[i]) {
            output += v + ' | ';
        }

        output += '\r\n';
        
        // Write table header horizontal divider
        for (const v of x[i]) {
            output += '| ----- ';
        }

        output += '\r\n';

    } else {

        // Write table values
        for (const v of x[i]) {
            output += v + ' | ';
        }

        output += '\r\n';
        
    }
}

console.log(output);

```

### Output

| id | make | model | 
| ----- | ----- | ----- 
| 1 | Fender | Stratocaster | 
| 2 | Fender | Telecaster | 
| 2 | Gibson | Les Paul | 


---



```
// JavaScript "fizzbuzz" example...

let c = 100;
let i = 1;

for(i < c; i < c; i++)  {
    f = i%3;
    b = i%5;
        
    if ( f == 0 && b == 0) {
        console.log(i, 'fizzbuzz');
    } else if(f == 0 && b != 0) {
        console.log(i, 'fizz');
    } else if(f != 0 && b == 0) {
        console.log(i, 'buzz');
    } else {
        console.log(i);
    }
}
```
