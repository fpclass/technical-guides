# Haskell IDE Engine

This guide explains how to install Haskell IDE Engine (or `hie` for short) on your own machine.

## General installation steps

This section contains general installation steps for Haskell IDE Engine which should be the same on all platforms (although are untested on Windows).

### Obtaining the code

Recent versions of `hie` need to be built from source, there are no pre-compiled binaries available. You can obtain the source code by running the following command (which may take a couple of minutes to complete due the amount of code that is being downloaded):

```bash
$ git clone https://github.com/haskell/haskell-ide-engine --recurse-submodules
```

### Compiling the code

Once the code has been downloaded, it needs to be built. By default, the scripts provided will try to build `hie` for all versions of GHC it supports. That would take up a lot of time and space, but is not required. Instead, we only need `hie` to support the version of GHC we are using for the module which is 8.4.3. We can do this by navigating into the `haskell-ide-engine` directory that will have been created by the previous `git clone` command and using the specific project configuration file for `stack` for the version of GHC we want to use. Note that this process may take a good 30 minutes or so:

```bash
$ cd haskell-ide-engine
$ stack build --stack-yaml=stack-8.4.3.yaml
```

### Installing the binaries

Once `hie` has been built for GHC 8.4.3, it needs to be installed. You can do this by running:

```bash
$ stack install --stack-yaml=stack-8.4.3.yaml
```

Note that especially on macOS, `stack` will install binaries into a directory that is not contained in your `$PATH` environment variable by default (`%PATH%` on Windows) and it may likely warn you about it. You can test whether `hie` has been installed into a directory that is in `$PATH` by running:

```bash
$ which hie
```

If a path to `hie` appears, it is located in a directory that is in `$PATH`. If you get no output, then it is not. In the latter case, you have two options:

1. Copy the binaries manually from the directory that `stack` has installed them into to a different directory that is in `$PATH`. You can check which directories are in `$PATH` by running:
```bash
$ echo $PATH
```
Pick a suitable directory and copy the `hie` and `hie-wrapper` executables into it. For example, on macOS, `stack` may install your binaries into `~/.local/bin` and `/usr/local/bin` is a directory that is in `$PATH` by default, so you can copy the `hie` binaries by running:
```bash
$ cp ~/.local/bin/hie* /usr/local/bin/
```
2. Include the directory that `stack` installs binaries to in your `$PATH` variable.

### Generating the documentation

The last step should be to generate the documentation that `hie` will show you when you hover over the name of library functions etc. To do this, run the following command in the `haskell-ide-engine` directory:

```bash
$ stack --stack-yaml=stack-8.4.3.yaml exec hoogle generate
```

Once completed, `hie` should be installed correctly on your machine for GHC 8.4.3.
