## Staying Connected to the Cloud

Depending on how you connect to the cloud, you may have processes and jobs that are
running, and will need to continue running for some time. If you are connecting to your
cloud desktop via VNC, jobs you start will continue to run. If you are connecting via SSH,
if you end the SSH connection (e.g. you exit your SSH session, you lose your connection
to the internet, you close your laptop, etc.), jobs that are still running when you
disconnect will be killed. There are a few ways to keep cloud processes running in the background.
Many times when we refer to a background process we are talking about what is
[described at this tutorial](http://www.cyberciti.biz/faq/linux-command-line-run-in-background/) -
running a command and returning to shell prompt. Here we describe a program that will
allow us to run our entire shell and keep that process running even if we disconnect: `tmux`. If you don't have `tmux` on your system, you should still be able to use `screen`. This is another program that has mostly the same capabilities as `tmux`. It's a lot older, though, so can be more clunky to use; however, it is likely to be available on any cloud system you encounter.

In both `tmux` and `screen`, you open a 'session'. A 'session' can be thought of as a window for `tmux` or `screen`, you might open an terminal to do one thing on the a computer and then open a new terminal to work on another task at the command line. 

As you work, an open session will stay active until you close this session. Even if you disconnect from your machine, the jobs you start in this session will run till completion.

For the following instructions use either `tmux` OR `screen`, not both!
{: .callout}

### Starting and attaching to a session

You can start a session and give it a descriptive name:

- `tmux`

  ~~~
  $ tmux new -s session_name
  ~~~
  {: .bash}

- `screen`

  ~~~
  $ screen -S session_name
  ~~~
  {: .bash}

This creates a session with the name `session_name` which will stay active until you close it.

### Detach session (process keeps running in background)

You can detach from a session by pressing on your keyboard:

- `tmux`: `control + b` followed by `d` (for detach)
- `screen`: `control + a` followed by `d` (for detach)

#### Seeing active sessions

If you disconnect from your session, or from your ssh into a machine, you will need to reconnect to an existing session. You can see a list of existing sessions:

- `tmux`

  ~~~
  $ tmux list-sessions
  ~~~
  {: .bash}

- `screen`

  ~~~
  $ screen -ls
  ~~~
  {: .bash}

#### Connecting to a session

To connect to an existing session:

- `tmux`

  ~~~
  $ tmux attach -t session_name
  ~~~
  {: .bash} 

  The `-t` option = 'target'

- `screen`

  ~~~
  $ screen -r session_name
  ~~~
  {: .bash}

  The `-r` option = 'resume  a detached screen session'

#### Switch sessions

You can switch between sessions:

- `tmux`

  ~~~
  $ tmux switch -t session_name
  ~~~
  {: .bash}

#### Kill a session

You can end sessions:

- `tmux`

  ~~~
  $ tmux kill-session -t session_name
  ~~~
  {: .bash}

- `screen`

  ~~~
  $ screen -r session_name
  $ exit
  ~~~
  {: .bash}
