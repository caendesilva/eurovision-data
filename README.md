# Eurovision Data

Datasets from the Eurovision Song Contest

Parsed from https://github.com/Spijkervet/eurovision-dataset by loading the CSV data into an array to work with.

## Source code

```php
function parseCsvData(string $csvText): array
{
    // Create a temporary file stream
    $fp = fopen('php://temp', 'r+');
    fputs($fp, $csvText);
    rewind($fp);

    // Read the CSV data from the stream
    $csv = [];
    while (($data = fgetcsv($fp)) !== false ) {
        $csv[] = $data;
    }
    fclose($fp);

    // Now make the first row the keys for the rest of the rows
    $keys = array_shift($csv);
    foreach ($csv as $i => $row) {
        $csv[$i] = array_combine($keys, $row);
    }

    return $csv;
}

$db = parseCsvData(file_get_contents('contestants.csv'));
```
