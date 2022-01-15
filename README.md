### `cue-unity/example`

[`unity`](https://github.com/cue-unity/unity) is a tool used to run experiments/regression tests on various CUE modules
using different versions of CUE.

`cue-unity/example` is a minimal example CUE project that defines a `unity` manifest and tests. `cue-unity/example` uses `unity`
to [test itself in a GitHub
workflow](https://github.com/cue-unity/example/blob/50254fe95093f9460a0e12debf7b4684763a1a5c/.github/workflows/test.yml#L27-L28),
and `cue-unity/example` is a [project in the `unity`
corpus](https://github.com/cue-unity/unity/tree/3ca7e170a42793a20104a3c82cb56d204e8894ed/projects/github.com/cue-unity).

### Understanding `cue-unity/example`

Like any project that is tested using `unity`, `cue-unity/example` declares its manifest as a CUE package value in
[`cue.mod/tests`](https://github.com/cue-unity/example/blob/50254fe95093f9460a0e12debf7b4684763a1a5c/cue.mod/tests/tests.cue)
that satisfies the
[`#Manifest`](https://github.com/cue-unity/unity/blob/de07b0f83e70913697b2f70f660db888d11059d4/unity_go_gen.cue#L9-L14)
definition:

```
package tests

Versions: ["go.mod", "v0.3.0-beta.5"]
```

Via this manifest, `cue-unity/example` declares the latest versions of CUE against which its configurations are known to be
correct, or more precisely against which its `unity` tests are known to pass.

The `cue.mod/tests` directory also contains a number of
[`testscript`](https://pkg.go.dev/github.com/rogpeppe/go-internal/testscript) test scripts. `cue-unity/example` defines a
basic
[`eval.txt`](https://github.com/cue-unity/example/blob/50254fe95093f9460a0e12debf7b4684763a1a5c/cue.mod/tests/eval.txt)
test script as follows:

```
# Verify that eval works as expect

cue eval ./...
cmp stdout $WORK/stdout.golden

-- stdout.golden --

x: 5
```

See the [`unity` README](https://github.com/cue-unity/unity/blob/main/README.md) for more information.
