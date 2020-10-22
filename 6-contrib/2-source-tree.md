# Source Tree Layout

The root directory of this project is organized as follows:

- `build`: platform dependent build files
- `contrib`: external modules, subsystems and libraries
- `doxygen`: config files for generating documentation out of the source code
- `img`: built-in image sources
- `include`: global header files
- `src`: source files
- `ssh`: ssh config files for the automated testing system
- `utils`: utility scripts for building and running this project

# Branches

The project is organized in different branches. We have three special
ones:

- The `master` branch is meant for stable code.

- The `unstable` branch is meant for code that is maturing.  I merge the
  `dev` branch onto `unstable` weekly.

- The `dev` branch is write protected, but you can submit pull requests
  to it. All your branches should derive from it.


If you are creating a branch to work on, stick to the following rules:

- Use `enhancement-<name>` to work enhancements
- Use `feature-<name>` to work on features
- Use `bugfix-<name>` to work on bug fixes
- Use `enhancement-<target>-<name>` to work on platform dependent enhancements
- Use `feature-<target>-<name>` to work on platform dependent features
- Use `bugfix-<target>-<name>` to work on platform dependent bug fixes
