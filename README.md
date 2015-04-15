# medit
Port and Modification of Pascal Frey's medit software for tet-mesh visualization

I'm not sure what the original license was for these files. There's [French
documentation](http://www.ann.jussieu.fr/frey/logiciels/Docmedit.dir/index.html)
and a related
[thesis](http://www.ann.jussieu.fr/frey/publications/RT-0253.pdf).

This tool is especially useful for examining the output of TetGen: `.mesh`
files.

## Compilation

I've `ifdef IGL` guarded all of my changes, so you can still compile the legacy
version.

Before compiling either version issue, compile `libmesh.a`

```bash
make -C libmesh/
```

### Adapted version

To compile the "new and improved" version. First install
[libigl](libigl.github.io/libigl/) and AntTweakBar (preferably from
`libigl/external/AntTweakBar`) and yimg (preferably from
`libigl/external/yimg/`)

> I've set up the make file to use the optional `IGL_STATIC_LIBRARY` flag. It
> should be possible to modify `Makefile.igl` to use the default header only
> version of libigl.

Then issue:

```bash
make -f Makefile.igl clean
make -f Makefile.igl
```

### Legacy

Issue

```bash
make clean
make
```

## Running

Pass a `.mesh` file to medit via the command line:

```bash
./medit input.mesh
```

## Development Notes
"Capping" seems to mean cutting a planar slice. *Not* the mountain top view. So
`capTetraMap` creates a display list for the planar slice view. And
`listTetraMap` creates one for the mountain top view.

`pXYZ` is a pointer to `XYZ`.

`pTransform` contains many members that are really just deltas (changes) in
axis-angle, pan etc.
