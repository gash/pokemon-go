# pokemon-go
2020.85: your programming language that is just a crappy wrapper for Go, where all the keywords are now Pokémon

## Running pokemon-go

You will need a Go compiler. To create the compiler, execute the command:
```
go build -o pokemon-go pokemon_go.go
```

To run the example code, `pokemon_go_example.pgo`:
```
./pokemon-go pokemon_go_example.pgo
go run temp.go
```

## How pokemon-go works

To ensure that we properly tokenize pokemon-go with correct substitution of keywords from Go, we copied over the contents of https://golang.org/src/go/token/token.go and changed the values of the tokens. We also had to create one new keyword, `importgo`.

### Mapping of keyword names

Please check out [this Google Sheet](https://docs.google.com/spreadsheets/d/14faEWc8WIfuvxUMHofM_e2u_xjuq0ke0zs2LCpffKLc/edit#gid=1415904394) for the mapping between all the different keywords in one convenient place.

### importgo

We considered just creating a whole new compiler called `pokemon-go` by changing that token file in the source directory and then building the entire compiler. However, many other Go packages rely on the `go` keywords and changing those keywords would break how Go processed those files. It would mean we would have to go and update many, if not every, `.go` file in the repository. Thus, we introduced two ways to import files: one for regular `.go` files and our new `.pgo` files.


## Converting from pokemon-go to Go

At the moment, pokemon-go functions as a translator by creating a temporary `temp.go` file and then the user executes that file. Because of the compiled nature of Go as a programming language, it is difficult to execute or evaluate code contained within a string in a program. Other more dynamics languages, like Javascript, have such potentialities natively built in. We are investigating a tigheter integration.

However, this loose integration DOES mean that we have access to all of Go's functionality. For example, one could easily run:
```
./pokemon-go pokemon_go_example.pgo
go run temp.go
```

## Converting from Go to pokemon-go

We have a utility that lets the user convert from Go to pokemon-go:
```
go build go2pgo.go
```

It can then be run as:
```
./go2pgo.go switch.go switch.pgo
```

The resulting code can then be run from pokemon-go.

## Improvements

We acknowledge that comments are not preserved during the conversion phase from Go to pokemon-go or vice versa.
