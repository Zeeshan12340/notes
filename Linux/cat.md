# cat
[https://unix.stackexchange.com/questions/297560/cat-into-stdin-then-pipe-into-program-keeps-forked-shell-open-why](https://unix.stackexchange.com/questions/297560/cat-into-stdin-then-pipe-into-program-keeps-forked-shell-open-why)

bypass forked shells

it has to do with the closing of the stdin. when you use cat like that it keeps stdin open which allows you to interact with the shell you get, for the cases where it "works", you are leaving a process running `**cat**` which is reading _its_ standard input, which has not been closed. Since that is not (yet) closed, `**cat**` continues to run, leaving _its_ standard output open, which is used by the shell (also not closed).