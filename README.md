# Temp
Temporary structs and maps with expiring elements in Golang

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents** 

- [Basic Usage](#basic-usage)
  - [Temporary struct](#temporary-struct)
  - [Expiring map](#expiring-map)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Basic Usage
## Temporary struct

```go
type session struct {
	ID string
	temp.T
}

func main() {
	sess := session{}
	temp.ExpireAfter(&sess, time.Second)
	fmt.Printf("Session expired: %v\n", temp.Expired(&sess)) // false
	time.Sleep(time.Second)
	fmt.Printf("Session expired: %v\n", temp.Expired(&sess)) // true
}

```


## Expiring map

```go
m := map[string]*session{
    "123": &session{
        ID: "123",
        T: T{
            expires: time.Now().Add(time.Second),
        },
    },
    "124": &session{
        ID: "124",
        T: T{
            expires: time.Now().Add(time.Second),
        },
    },
    "125": &session{
        ID: "125",
        T: T{
            expires: time.Now().Add(time.Second),
        },
    },
}
go Clean(m, time.Millisecond*50) //Clean blocks forever
time.Sleep(time.Second * 2)
//Map should be empty here
```

