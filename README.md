# unln

`unln` allows the user to remove symlinks as well as their targets depending on the options set. It is possible to leave the targets untouched, remove the targets based on whether they themselves are links or non-link files, as well as recursively remove targets that are links to a specified level.

As an additional feature, it is also possible to remove non-link files by directly passing them to `unln` as well (provided the appropriate option is set). The latter feature is added for ease of use to provide the ability to remove both link and non-link files within a single operation.

Also see a related tool [`reln`](https://github.com/linguisticmind/reln) for moving or copying symlinks while automatically adjusting their targets.

Video tutorial:

[![Mindful Technology - reln, unln: move symlinks fixing paths to targets, delete symlinks *and* their targets, and more](https://img.youtube.com/vi/jAlPWsBIhMM/0.jpg)](https://www.youtube.com/watch?v=jAlPWsBIhMM)

## Changelog

<table>
    <tr>
        <th>Version</th>
        <th>Date</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>
            <a href="https://github.com/linguisticmind/unln/releases/tag/v0.1.0">0.1.0</a>
        </td>
        <td>
            2024-05-17
        </td>
        <td>
            <p>
                Initial release.
            </p>
        </td>
    </tr>
</table>

[Read more](CHANGELOG.md)

## Dependencies

`unln` was written and tested on Debian 12, and takes advantage of standard utilities that come with the system. In order to run `unln` on other systems, make sure that the following are installed and available on system's `PATH`:

* Bash >= 5.2.15
* Enhanced getopt
* GNU coreutils
* GNU sed

## Installation

1. Clone this repository to a directory of your choice (e.g. `~/repos`):

    ```bash
    cd ~/repos
    git clone https://github.com/linguisticmind/unln.git
    ```

2. Symlink or copy the [script file](unln) to a directory on your `PATH` (e.g. `~/bin`):

    ```bash
    cd ~/bin
    # To symlink:
    ln -sv ../repos/unln/unln
    # To copy:
    cp -av ../repos/unln/unln .
    ```

3. (OPTIONAL) Symlink or copy the [man page](man/man1/unln.1) to a directory on your `MANPATH` (e.g. `~/man`):

    ```bash
    cd ~/man/man1 # The `man` directory should contain subdirectories for different manual sections: `man1`, `man2` etc.
    # To symlink:
    ln -sv ../../repos/unln/man/man1/unln.1
    # To copy:
    cp -av ../../repos/unln/man/man1/unln.1 .
    ```

    A copy of the manual page is also [included in this README file](#manual).

4. (OPTIONAL) Copy the [example config file](config.bash) to the config directory:

    ```bash
    mkdir -v ~/.config/unln
    cp -v ~/repos/unln/config.bash ~/.config/unln
    ```

## Manual

```plain
UNLN(1)                     General Commands Manual                    UNLN(1)

NAME
       unln - remove symlinks and their targets

SYNOPSIS
        unln [<options>] <link|file> ...

DESCRIPTION
       unln  allows  the  user to remove symlinks as well as their targets de‐
       pending on the options set. It is possible to  leave  the  targets  un‐
       touched,  remove the targets based on whether they themselves are links
       or non-link files, as well as recursively remove targets that are links
       to a specified level.

       As  an additional feature, it is also possible to remove non-link files
       by directly passing them to unln as well (provided the appropriate  op‐
       tion  is  set).  The latter feature is added for ease of use to provide
       the ability to remove both link and non-link files within a single  op‐
       eration.

OPTIONS
   Passing arguments to options
       Enhanced  getopt  syntax applies when passing options. There is one im‐
       portant point to highlight when it comes to passing  options  with  re‐
       quired vs optional arguments.

       In  case  of  a short option, if an option takes a *required* argument,
       the argument may be written as a separate parameter, *or* directly  af‐
       ter  the  option  character. If an option takes an *optional* argument,
       however, the argument *must* be written directly after the option char‐
       acter.

       In case of a long option, if an option takes a *required* argument, the
       argument may be written as a separate parameter,  *or*  directly  after
       the  option name, separated by an equals sign (`=`). If an option takes
       an *optional* argument, however, the argument *must*  be  writtent  di‐
       rectly after the option name, separated by an equals sign (`=`).

                           Short option   Long option
       Required argument   -o <value>     --option <value>
                           -o<value>      --option=<value>
       Optional argument   -o[<value>]    --option[=<value>]

       Options  that  take optional arguments can be recognized in the options
       list below by their <value> and the preceding  equals  sign  being  en‐
       closed in square brackets:

       -o, --option[=<value>]

   General
       -r, --run
              Perform the specified operations instead of simulating them.

       -R, --no-run
              Simulate  the  specified  operations instead of performing them.
              This is the default.

       -p, --print-cmd
              Print a preview of the commands to be executed.

       -P, --no-print-cmd
              Do not print a preview of the commands to be executed.  This  is
              the default.

       -t, --remove-targets[={links|files|all|none}]
              Remove targets of the specified type.

              links  Remove targets that are links.

              files  Remove targets that are non-link files.

              [all]  Remove both the targets that are links and those that are
                     non-link files.

              none (default)
                     Do not remove targets. Equivalent to -T, --no-remove-tar‐
                     gets.

       -T, --no-remove-targets
              Do not remove targets. Equivalent to -t, --remove-targets set to
              `none`.

       -f, --remove-files
              Remove non-link files passed as positional arguments to unln.

       -F, --no-remove-files
              Do not remove non-link files passed as positional  arguments  to
              unln. This is the default.

       -L, --dereference-targets[={<integer>|inf}]
              Dereference  link targets to a specified level for recursive re‐
              moval. The default value is `0`.

              The value can be an integer greater than or equal to  0,  `inf`,
              or no value. Omitting the value is equivalent to passing `inf`.

   Other
       -c, --color
              Colorize the output. This is the default.

       -C, --no-color
              Disable colorization of the output.

       -h, --help
              Print help.

       -V, --version
              Print version information.

FILES
       A configuration file can be used to set default options.

       The configuration file's location is $XDG_CONFIG_HOME/unln/config.bash.
       If XDG_CONFIG_HOME is not set, it defaults to ~/.config.

AUTHOR
       Alex Rogers <https://github.com/linguisticmind>

HOMEPAGE
       <https://github.com/linguisticmind/unln>

COPYRIGHT
       Copyright © 2023 Alex Rogers. License GPLv3+:  GNU  GPL  version  3  or
       later <https://gnu.org/licenses/gpl.html>.

       This  is  free  software:  you  are free to change and redistribute it.
       There is NO WARRANTY, to the extent permitted by law.

UNLN 0.1.0                           2024                              UNLN(1)
```

## License

[GNU General Public License v3.0](LICENSE)
