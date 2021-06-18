[//title]: (go-write-csv-to-file)
[//englishtitle]: (go-write-csv-to-file)
[//category]: (go,snippet)
[//tags]: (go,snippet)
[//createtime]: (20210615)
[//updatetime]: (20210615)

```go
package main

import (
	"encoding/csv"
	"log"
	"os"
)

func main() {
	rows := [][]string{
		{"Name", "City", "Language"},
		{"Pinky", "London", "Python"},
		{"Nicky", "Paris", "Golang"},
		{"Micky", "Tokyo", "Php"},
	}

	csvfile, err := os.Create("test.csv")
	defer func() {
		csvWriter.Flush()
		_ = csvFile.Close()
	}()
	if err != nil {
		log.Fatalf("failed creating file: %s", err)
	}

	csvwriter := csv.NewWriter(csvfile)

	for _, row := range rows {
		_ = csvwriter.Write(row) // if write concurrently, use sync.Mutex for lock & write
	}
}
```

## context

sometimes I need to log struct data, but don't want to use db, so csv is a lightweight choose.

## reference

[Golang write CSV records](https://www.golangprograms.com/golang-write-csv-records.html)
