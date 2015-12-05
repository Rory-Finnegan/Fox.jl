Fox.jl
============
[![Build Status](https://travis-ci.org/Rory-Finnegan/Fox.jl.svg?branch=master)](https://travis-ci.org/Rory-Finnegan/Fox.jl)

A package for running tests in julia playgrounds like tox does with virtualenvs. It currently attempts to parse the `julia` and `script` parts the 
`.travis.yml` in your project root directory. Alternatively, you can place the julia and script sections in a `fox.yml` file, which will take priority when running `fox`.


== Installation ==
Install the julia package
```shell
julia> Pkg.clone("https://github.com/Rory-Finnegan/Fox.jl")
```

== Usage ==

```shell
fox
```

Will build all playgrounds in `.fox/` named by the julia version being tested.

You can also specify a subset of the julia versions listed in your travis file at the command line with
```shell
fox -j julia-0.4, julia-latest
```

== Config ==
Fox searches for a fox.yml file in the local directory (`./fox.yml`), followed by the user directory (`~/fox.yml`) and finally the system directory (`/etc/fox.yml`).

```yaml
# content of: fox.yml (or the julia and script sections of a travis file)
julia:
    - 0.4
    - 0.5


script:
    - julia -e 'Pkg.init(); Pkg.clone(pwd()); Pkg.test("PkgName")'
```

NOTE: The julia versions provided must be installed via Playground.jl with the corresponding label in order for fox to test against it. If you labelled your julia versions with the format of `julia-0.4` fox will handle stripping off the `julia-`.
