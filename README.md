# Specifics of this fork

This is a fork of https://github.com/caseyscarborough/keylogger

I have made some modifications for my personal use. I'm putting them out here as maybe someone else might find the useful.

The modifications are:

* Drops root privileges when run with `sudo`.
* Logs milliseconds since Epoch for each keystroke.
* Adds newline after each log entry.

Because of the design of OSX, to log keystrokes properly, `keylogger` needs to run with root privileges. I have solved this by using `sudo`. There's probably better ways that I'm not aware of.

To use `sudo` without password for `keylogger` you need to add something similar to this to your `/etc/sudoers` file using `visudo`.

```
albin ALL=(root) NOPASSWD: /Users/albin/bin/keylogger`
```

> Note: You need to change the path of your logfile in `keylogger.h`.


# Mac OS X Keylogger

This repository holds the code for a simple and easy to use keylogger for Mac OS X. It is not meant to be malicious, and is written as a proof of concept. There is not a lot of information on keyloggers or implementing them on Mac OS X, and most of the ones I've seen do not work as indicated. This project aims to be a simple implementation on how it can be accomplished on OS X.

> Note: This keylogger is currently unable to capture secure input such as passwords. See issue #3 for more information.

## Usage

Start by cloning the repository and running the proper make commands, shown below. By default, the application installs to `/usr/local/bin/keylogger`, which can easily be changed in the [`Makefile`](https://github.com/caseyscarborough/keylogger/blob/master/Makefile). `make install` may require root access.

```bash
$ git clone https://github.com/caseyscarborough/keylogger && cd keylogger
$ make && make install
```

The application by default logs to `/var/log/keystroke.log`, which may require root access depending on your system's permissions. You can change this in [`keylogger.h`](https://github.com/caseyscarborough/keylogger/blob/master/keylogger.h#L12) if necessary.

```bash
$ keylogger
Logging to: /var/log/keystroke.log
```

If you'd like the application to run on startup, run the `startup` make target:

```bash
$ sudo make startup
```

## Uninstallation

You can completely remove the application from your system (including the startup daemon) by running the following command (logs will not be deleted):

```bash
$ sudo make uninstall
```

### Optional Parameters

You can pass in two optional parameters to the program. The `clear` option will clear the logs at the default location. Any other argument passed in will be used as the path to the log file for that process. See below:

```bash
# Clear the logfile.
$ keylogger clear
Logfile cleared.

# Specify a logfile location.
$ keylogger ~/logfile.txt
Logging to: /Users/Casey/logfile.txt
```

## Contributing

Feel free to fork the project and submit a pull request with your changes!
