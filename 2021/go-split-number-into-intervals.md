[//title]: (go-split-number-into-intervals)
[//englishtitle]: (go-split-number-into-intervals)
[//category]: (go,snippet)
[//tags]: (go,goroutine,snippet)
[//createtime]: (20210622)
[//updatetime]: (20220923)

Split number into intervals, so that each go routine can concurrent process part of the job.

```go
func ToIntervals(start int64, end int64, interval int64) (intervals [][2]int64, err error) {
	if start > end {
		return nil, errors.New(fmt.Sprintf("invalid input %d %d %d, start > end", start, end, interval))
	}
	if interval < 0 {
		return nil, errors.New(fmt.Sprintf("invalid input %d %d %d, interval <= 0", start, end, interval))
	}
	if interval == 0 || interval > end-start {
		return [][2]int64{{start, end}}, nil
	}
	for i := start; i <= end; i += interval {
		if i+interval-1 > end {
			intervals = append(intervals, [2]int64{i, end})
			break
		}
		intervals = append(intervals, [2]int64{i, i + interval - 1})
	}
	return intervals, nil
}
```

Test

```go
func TestToIntervals(t *testing.T) {
	intervals, err := ToIntervals(0, 10, 3)
	t.Log(intervals, err) // [[0 2] [3 5] [6 8] [9 10]]
}
```
