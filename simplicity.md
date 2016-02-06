# simplicity

The simplicity project aims to simplify life by breaking habits.

## Background

Tools such as [foo](foo) gives an indication of where you spend your time. But even with this knowledge it is sometimes difficult to break habits. My own habits include saving after every few keystrokes, checking `thunderbird` several times in a day and restarting `stunnel` too often. They used to include checking a range of web pages for updates but this activity have been superseded by the use of [nyfiken](https://github.com/karlek/nyfiken). My developing `nyfiken` addiction is another story.

It is clear that some of these activities are habits; for instance I restart `stunnel` to work around a DNS lookup bug which may have been fixed already. Nowadays I simply run and re-run the command out of habits, not for its intended outcome. While not all habits are bad some take a lot of time or worse still, break our concentration.

## Ideas

* Command timeout

Specify timeout for commands, e.g:

`ini
[thunderbird]
timeout=22h
`

With this configuration if `thunderbird` is executed more than once within the scope of 22 hours, display a "Please wait for another 12h" message instead.

* Web page blacklist

Specify blacklisted web pages, e.g:

`ini
[youtube.com]
blacklist=true
`

With this configuration network requests to `youtube.com` will be terminated.

* ...

There are definitely habits which cannot be broken using the above ideas. What other kind of habits do we fall into that could benefit from a systematic breakdown? If you've got an idea or want to start a discussion, please feel free! Use the issues, pull requests or simply comment on a commit message or send an email :)

## Implementation approaches

* Command timeout

1) Aliases

A very simple approach to enforce command timeouts would be to use aliases, e.g.

```bash
alias thunderbird="simplicity thunderbird"
```

The simplicity command could check when `thunderbird` was last executed and either forward the request or display a "Please wait ..." message.

One problem with this approach is that it is very easy to circumvent, simply execute `/usr/bin/thunderbird` instead of `thunderbird`.

2) `PATH`

A similar approach is to update the `PATH` environment variable to favour simplicity over the original executable, e.g.

```bash
export PATH=~/.config/simplicity/bin:$PATH
ln -s /path/to/simplicity ~/.config/simplicity/bin/thunderbird
```

This approach is equally easy to circumvent using `/usr/bin/thunderbird` instead of `thunderbird`.

3) Root kit (file path)

Restrict file access using root kit techniques. Intercept all file access requests from the user land and deny those that are on timeout.

The major benefit to this approach is that it is harder to circumvent, but it is not without drawbacks. The implementation will be much less portable, the error message will less friendly, e.g. "Permission denied." instead of "Please wait ..." (probably hackable ^^) and it seems like overkill for this problem.

This approach would successfully block symlink access but a copy of the executable would circumvent the restriction, e.g.

```bash
cp /usr/bin/thunderbird /tmp/foo && /tmp/foo
```

4) Root kit (file hashsum)

Instead of relying on the executable's file path, its hashsum could be used for identification.

The main benefit would be that the file copy approach would no longer circumvent the restriction. However, this may have a huge performance impact and the hashsums needs to be updated with every new release of the software. Failing to do so would allow access to supposedly blocked commands, as the hashsum of the updated version is no longer on the blacklist.

5) Root kit (whitelist)

Instead of using a hashsum blacklist, a whitelist could be used.

I do like this approach as it provides security at the same time as it simplifies life. The drawback is that it will inevitably make life more difficult in other regards, such as compiling and playing with new commands and libraries. It is possible that a development environment could be created to mitigate this issue, but that approach may enable new circumvention methods.

Similarly to the blacklist, the whitelist hashsums needs to be keep up to date. Failing to do so may render the system unusable after a software update, as previously allowed commands now have invalid hashsums.

6) ...

None of the suggested approaches feels like the right one. Every methods has its own benefits and drawbacks, ranging from ease of implementation and complexity to robustness and usability.

If you have an idea or would like to discuss an alternative approach, please feel free! I'd be eager to get some input! As already mentioned, use a combination of pull requests, issues, comments on commits or email messages to get the conversation going.

## Public domain

The source code and any original content of this repository is hereby released into the [public domain].

[public domain]: https://creativecommons.org/publicdomain/zero/1.0/
