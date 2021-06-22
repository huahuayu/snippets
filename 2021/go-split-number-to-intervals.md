```go
func toIntervals(number int64, interval int64) (intervals [][2]int64, err error) {
	if !(number >= 1 && interval > 0) {
		return nil, errors.New("invalid input")
	}
	if number <= interval {
		return [][2]int64{{0, number - 1}}, nil
	}
	var (
		prev int64 = 0
		next       = interval - 1
		max        = number - 1
	)
	for {
		intervals = append(intervals, [2]int64{prev, next})
		prev = next + 1
		next = next + interval
		if next >= max {
			next = max
			intervals = append(intervals, [2]int64{prev, next})
			break
		}
	}
	return intervals, nil
}
```

```go
func TestToIntervals(t *testing.T) {
	intervals ,err:= toIntervals(10, 3)
	fmt.Println(intervals,err) // [[0 2] [3 5] [6 8] [9 9]] <nil>
}
```

## context

split number to intervals for each go routine to parallel process
