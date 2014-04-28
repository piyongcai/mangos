## mangos

[![GoDoc](https://godoc.org/bitbucket.org/gdamore/mangos?status.png)](https://godoc.org/bitbucket.org/gdamore/mangos)

package mangos is an implementation in pure Go of the SP ("Scalable Protocols")
protocols.  This makes heavy use of go channels, internally, but it can operate
on systems that lack support for cgo.  It has no external dependencies.

The reference implementation of the SP protocols is available as
[nanomsg](http://www.nanomsg.org)
 
The design is intended to make it easy to add new transports with almost trivial
effort, as well as new topologies ("protocols" in SP terminology.)

At present, all of the Req/Rep, Pub/Sub, Pair, Bus, Push/Pull, and
Surveyor/Respondent patterns are supported.

Additionally, there is an experimental new pattern called STAR available.  This
pattern is like Bus, except that the messages are delivered not just to
immediate peers, but to all members of the topology.  Developers must be careful
not to create cycles in their network when using this pattern, otherwise
infinite loops can occur.

Supported transports include TCP, inproc, IPC, and TLS.  TLS support is
experimental.  Use addresses of the form "tls+tcp://<host>:<port>" to access it.
Note that ipc:// is not supported on Windows (by either this or the reference
implementation.)  Forcing the local TCP port in Dial is not supported yet (this
is rarely useful).

Basic interoperability with nanomsg has been tested with nanocat.

Consider this a work-in-progress, and use at your own risk.

If you find this useful, I would appreciate knowing about it.  I can be reached
via my email address, garrett -at- damore -dot- org

## Installing

### Using *go get*

    $ go get bitbucket.org/gdamore/mangos

After this command *mangos* is ready to use. Its source will be in:

    $GOPATH/src/pkg/bitbucket.org/gdamore/mangos

You can use `go get -u -a` to update all installed packages.

## Documentation

For docs, see http://godoc.org/bitbucket.org/gdamore/mangos or run:

    $ godoc bitbucket.org/gdamore/mangos

## Testing

This package supports internal self tests, which can be run in
the idiomatic Go way, although it uses a separate test sub-package:

    $ go test bitbucket.org/gdamore/mangos/test

There are also internal benchmarks available:

	$ go test -bench=. bitbucket.org/gdamore/mangos/test

Enjoy!
