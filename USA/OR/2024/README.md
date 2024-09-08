This file contains TSV data for the upcoming Oregon General Election on November 5th, 2024.

### Ballot Measures

All counties and sourced from https://secure.sos.state.or.us/orestar/gotoLocalMeasSearch.do on Saturday, Sept 7 2024 9:55pm PT.

### Candidates

Candidates were based on filings that weren't disqualified at the time I pulled them in, around 10:15pm the same day.

I used this PHP code to adjust multi-line answers and replaced the "\n" with "; ":

```php

$o = fopen("officials.tsv", "r");

$lines = [];

// read the file line by line.  trim each line.  if the line starts with "2024 General Election", then prefix a newline character.
$line = '';
while (!feof($o)) {
    $segment = trim(fgets($o));
    if (strpos($segment, "2024 General Election") === 0) {
        $lines[] = $line;
        $line = $segment;
    } else {
        $line .= '; ' . $segment;
    }
}

// close the file
fclose($o);

// Loop through each line and let's remove the PII columns
$colsToOmit = array(35, 36, 41, 42, 47, 48, 49, 50, 51);
foreach ($lines as $key => $line) {
    $cols = explode("\t", $line);
    if ($key != 0) {
        foreach ($colsToOmit as $col) {
            $cols[$col] = "redacted";
        }
    }
    $line2 = implode("\t", $cols);
    echo $line2 . "\n";
}
```
