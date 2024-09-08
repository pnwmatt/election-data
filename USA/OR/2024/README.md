This file contains TSV data for the upcoming Oregon General Election on November 5th, 2024.

### Ballot Measures

All counties and sourced from https://secure.sos.state.or.us/orestar/gotoLocalMeasSearch.do on Saturday, Sept 7 2024 9:55pm PT.

### Candidates

Candidates were based on filings that weren't disqualified at the time I pulled them in, around 10:15pm the same day.

I used this PHP code to adjust multi-line answers and replaced the "\n" with "; ":

```php
<?php

$o = fopen("officials.tsv", "r");

// read the file line by line.  trim each line.  if the line starts with "2024 General Election", then prefix a newline character.
while (!feof($o)) {
    $line = trim(fgets($o));
    if (strpos($line, "2024 General Election") === 0) {
        echo "\n" . $line;
    } else {
        echo "; " . $line;
    }
}

// close the file
fclose($o);
echo "\n";
```