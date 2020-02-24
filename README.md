# sedbot

forked from [clsr/sedbot](https://github.com/clsr/sedbot) -
updated for `-i`'s new argument requirement and daemonized

sedbot is an IRC search-replace bot written using bash and sed.

### usage

1. `cp .cfg{.example,}`
1. adjust as needed
1. `bash sedbot.bash`

### daemonization

1. adjust sedbot.service
1. `mkdir -p ~/.config/systemd/user`
1. `cp sedbot.service ~/.config/systemd/user/`
1. `systemctl --user daemon-reload`
1. `systemctl --user enable --now sedbot`

### authenticate to services

1. `cp account.ini{.sample,}`
1. fill in your credentials
1. restart the bot (`systemctl --user restart sedbot`)


Only the s command and g and i flags are supported. Multiple regular expressions can be used at once, delimit them with spaces in between the flags and the s next one's s command. The last one may omit the trailing / if it has no options.

Example usage in chat:

    <foo> Hello ther!
    <foo> s/ther/there
    <sedbot> <foo> Hello there!

    <foo> I'm programmign right now
    <bar> foo: s/gn/ng/
    <sedbot> <foo> I'm programming right now

    <foo> abcdefghi
    <foo> s/\(.\)./\u\1/g s/
    <sedbot> <foo> ACEGi
    <foo> s/[a-e]//g s/\(.\)\(.\)/\2\1
    <sedbot> <foo> gfhi

Note that the bot uses the standard grep (POSIX) regular expressions, i.e. use `.\+` and `\(foo\)\?` instead of `.+` and `(foo)?` as you'd do in egrep or other regex engines. Backreferences are written like `s/\(.\)/\1`, where `\1` matches the first capturing group. [Read more about sed regular expressions.](https://www.gnu.org/software/sed/manual/html_node/Regular-Expressions.html)

