# tcl-build-extension

This action build a Tcl or Tk extension. It is intended to be used in
conjunction with the [tcl-setup](https://github.com/apnadkarni/tcl-setup)
action which sets up a Tcl and Tk build environment and
[Tcl extension workflow templates](https://github.com/apnadkarni/tcl-extension-template#github-action-workflows).
The action assumes the extension uses the TEA framework to do autoconf
or nmake based builds.

# Usage

The `TCLINSTALLDIR` environment variable should be set to the Tcl
installation directory before calling this action. If the
[tcl-setup](https://github.com/apnadkarni/tcl-setup) action is
used to set up the Tcl environment, this is automatically done
by that action.

The `tcl-build-extension` action will

* Checkout the extension from the source repository including submodules
if any.

* Build the extension using the specified toolchain and options.

* Optionally, run the test suite.

Example:

```yaml
- name: Build extension
  uses: apnadkarni/tcl-build-extension
  with:
    # The tool chain to use. Only used on Windows. Must be 'vc' for Visual C++
    # or 'msys2' for MingW64. Required on Windows.
    toolchain: 'vc'

    # Additional options to pass to configure. Only used for autoconf
    # based builds. Optional.
    config-opts:

    # Additional options to pass to make or nmake. Optional.
    make-opts:

    # Additional options to pass to make or nmake test target. Optional.
    test-opts:

    # Name of subdirectory to use for builds. This can be used
    # by caller when the extension is built in multiple configurations
    # in a single run, for example with different libraries. Not
    # used with nmake.
    build-subdir:

    # Boolean to control whether tests are run. Optional. Defaults to true.
    run-tests: true
```

See [Tcl extension workflow templates](https://github.com/apnadkarni/tcl-extension-template#github-action-workflows)
for a complete example.

