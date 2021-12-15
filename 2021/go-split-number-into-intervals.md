[//title]: (go-split-number-into-intervals)
[//englishtitle]: (go-split-number-into-intervals)
[//category]: (go,snippet)
[//tags]: (go,goroutine,snippet)
[//createtime]: (20210622)
[//updatetime]: (20210623)

```go
package util

import "errors"

func ToIntervals(number int64, start int64, interval int64) (intervals [][2]int64, err error) {
	if !(number > 0 && interval > 0 && start < number) {
		return nil, errors.New("invalid input")
	}
	if start == number {
		return [][2]int64{}, nil
	}
	var (
		prev = start
		next = start + interval - 1
		max  = number - 1
	)
	if next > max {
		return [][2]int64{{prev, max}}, nil
	}
	for {
		intervals = append(intervals, [2]int64{prev, next})
		prev = next + 1
		next = next + interval
		if next >= max {
			intervals = append(intervals, [2]int64{prev, max})
			break
		}
	}
	return intervals, nil
}
```

test

```go
func TestToIntervals(t *testing.T) {
	intervals ,err:= toIntervals(10, 3)
	fmt.Println(intervals,err) // [[0 2] [3 5] [6 8] [9 9]] <nil>
}
```

## context

split number to intervals for each go routine to parallel process part of job

if with a start point in the middle

```go
func toIntervals(number int64, start int64, interval int64) (intervals [][2]int64, err error) {
	if !(number > 0 && interval > 0 && start < number) {
		return nil, errors.New("invalid input")
	}
	if start == number {
		return [][2]int64{}, nil
	}
	var (
		prev = start
		next = start + interval - 1
		max  = number - 1
	)
	if next > max {
		return [][2]int64{{prev, max}}, nil
	}
	for {
		intervals = append(intervals, [2]int64{prev, next})
		prev = next + 1
		next = next + interval
		if next >= max {
			intervals = append(intervals, [2]int64{prev, max})
			break
		}
	}
	return intervals, nil
}
```

test

```go
func TestToIntervals(t *testing.T) {
	intervals ,err:= toIntervals(10, 3, 3)
	fmt.Println(intervals,err) // [[3 5] [6 8] [9 9]] <nil>
}
```
