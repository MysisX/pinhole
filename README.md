# `pinhole`

<a href="https://godoc.org/github.com/tidwall/pinhole"><img src="https://img.shields.io/badge/api-reference-blue.svg?style=flat-square" alt="GoDoc"></a>


3D Wireframe Drawing Library for Go

<img src="http://i.imgur.com/mYfYtsI.jpg" width="300" height="300"><img src="http://i.imgur.com/WtGLS2P.jpg" width="300" height="300">
<img src="http://i.imgur.com/SuviZSA.jpg" width="300" height="300"><img src="http://i.imgur.com/Wvs25iH.jpg" width="300" height="300">

## Why does this exist?

I created this because I needed a software based 3D rendering library with a very simple API for visualizing data structures.

## Getting Started

### Installing

To start using `pinhole`, install Go and run `go get`:

```sh
$ go get -u github.com/tidwall/pinhole
```

This will retrieve the library.

### Using

The coordinate space has a locked origin of `0,0,0` with the min/max boundaries or `-1,-1,-1` to `+1,+1,+1`.
The `Z` coordinate extends from `-1` (nearest) to `+1` (farthest).

There are three types of shapes; `line`, `circle`, and `dot`. 
These can be transformed with the `Scale`, `Rotate`, and `Translate` functions.
Multiple shapes can be transformed by nesting in a `Begin/End` block.


A simple cube:

```go
p := pinhole.New()
p.DrawLine(-0.3, -0.3, -0.3, -0.3, -0.3, 0.3)
p.DrawLine(0.3, -0.3, -0.3, 0.3, -0.3, 0.3)
p.DrawLine(0.3, 0.3, -0.3, 0.3, 0.3, 0.3)
p.DrawLine(-0.3, 0.3, -0.3, -0.3, 0.3, 0.3)
p.DrawLine(-0.3, -0.3, -0.3, 0.3, -0.3, -0.3)
p.DrawLine(0.3, -0.3, -0.3, 0.3, 0.3, -0.3)
p.DrawLine(0.3, 0.3, -0.3, -0.3, 0.3, -0.3)
p.DrawLine(-0.3, 0.3, -0.3, -0.3, -0.3, -0.3)
p.DrawLine(-0.3, -0.3, 0.3, 0.3, -0.3, 0.3)
p.DrawLine(0.3, -0.3, 0.3, 0.3, 0.3, 0.3)
p.DrawLine(0.3, 0.3, 0.3, -0.3, 0.3, 0.3)
p.DrawLine(-0.3, 0.3, 0.3, -0.3, -0.3, 0.3)
p.SavePNG("cube.png", 500, 500)
```

<img src="http://i.imgur.com/ofJ2T7Y.jpg" width="300" height="300">


Rotate the cube:

```go
p := pinhole.New()
// ... omited DrawLines
p.Rotate(math.Pi/3, math.Pi/6, 0)
p.SavePNG("cube.png", 500, 500)
```

<img src="http://i.imgur.com/UewuE4L.jpg" width="300" height="300">

Add, rotate, and transform a circle:

```go
p := pinhole.New()
// ... omited DrawLines
p.Rotate(math.Pi/3, math.Pi/6, 0)

p.Begin()
p.DrawCircle(0, 0, 0, 0.2)
p.Rotate(0, math.Pi/2, 0)
p.Translate(-0.6, -0.4, 0)
p.Colorize(color.RGBA{255, 0, 0, 255})
p.End()

p.SavePNG("cube.png", 500, 500)
```

<img src="http://i.imgur.com/UafJsKW.jpg" width="300" height="300">

## Contact

Josh Baker [@tidwall](http://twitter.com/tidwall)

## License

`pinhole` source code is available under the ISC [License](/LICENSE).
