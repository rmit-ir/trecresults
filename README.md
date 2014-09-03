
# trecresults
    import "github.com/TimothyJones/trecresults"

Package trecresults provides helper functions for reading and writing trec results files
suitable for using with treceval







## type Result
``` go
type Result struct {
    Topic     int64   // the integer topic ID
    Iteration string  // the iteration this run is associated with (ignored by treceval)
    DocId     string  // the document ID for this result
    Rank      int64   // the rank in the result list
    Score     float64 // the score the document received for this topic
    RunName   string  // the name of the run this result is from
}
```
Describes a single entry in a trec result list









### func ResultFromLine
``` go
func ResultFromLine(line string) (*Result, error)
```
Creates a result structure from a single line from a results file
Returns parsing errors if any of the integer or float fields do not parse
Returns an error if there are not 6 fields in the result line
On error, a nil result is returned




### func (\*Result) String
``` go
func (r *Result) String() string
```
Formats a result structure into the original string representation that can be used with treceval



## type ResultFile
``` go
type ResultFile struct {
    Results map[int64]ResultList
}
```
Type definition for a result file
The result file supports multiple topics









### func NewResultFile
``` go
func NewResultFile() *ResultFile
```

### func ResultsFromReader
``` go
func ResultsFromReader(file io.Reader) (ResultFile, error)
```
This function returns a silce of results created from the
provided reader (eg a file).
On errors,a slice of every result read up until the error was encountered is
returned, along with the error




### func (ResultFile) NormaliseLinear
``` go
func (r ResultFile) NormaliseLinear()
```
This function normalises the runs of all result lists in this result file



### func (ResultFile) RenameRun
``` go
func (r ResultFile) RenameRun(newName string)
```
This function renames the runs of all result lists in this result file



### func (ResultFile) Sort
``` go
func (r ResultFile) Sort()
```
This function sorts all result lists in this result file



## type ResultList
``` go
type ResultList []*Result
```
Type definition for a result list











### func (ResultList) Len
``` go
func (r ResultList) Len() int
```
Functions for sorting a result list by score



### func (ResultList) Less
``` go
func (r ResultList) Less(i, j int) bool
```
Results are sorted first score (decreasing)



### func (ResultList) NormaliseLinear
``` go
func (r ResultList) NormaliseLinear()
```
This function operates on a slice of results, and normalises the score
of each result by score (score - min)/(max - min). This puts scores
in to the range 0-1, where 1 is the highest score, and 0 is the lowest.

No assumptions are made as to whether the slice is pre sorted



### func (ResultList) RenameRun
``` go
func (r ResultList) RenameRun(newName string)
```
This function renames all results in this run. Useful for giving a run a new name
after manipulation



### func (ResultList) Swap
``` go
func (r ResultList) Swap(i, j int)
```








- - -
Generated by [godoc2md](http://godoc.org/github.com/davecheney/godoc2md)
