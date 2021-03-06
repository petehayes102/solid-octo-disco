# Cord

Cord is a data streaming platform for composing, aggregating and distributing arbitrary
streams. It uses a publish-subscribe model that allows multiple publishers to share their
streams via a [Cord Broker](https://github.com/cord-proj/cord-broker). Subscribers can
then compose custom sinks using a regex-like pattern to access realtime data based on
their individual requirements.

To interact with the Broker, Cord provides the
[Cord Client](https://github.com/cord-proj/cord-client), which comprises a library and a
CLI. As the project matures, this library will form the basis of a suite of adaptors for
common technologies.

## Crates

Cord comprises three crates:

1.  **[Cord Broker](https://github.com/cord-proj/cord-broker)** - the server binary that
    aggregates and distributes arbitrary streams
2.  **[Cord Client](https://github.com/cord-proj/cord-client)** - provides a library and
    CLI for interacting with Cord brokers
3.  **[Cord Message](https://github.com/cord-proj/cord-message)** - an internal crate
    that defines the message envelope and codec for transmitting messages over the wire

## Usage

First, start a new [Cord Broker](https://github.com/cord-proj/cord-broker):

**Docker**

    $ docker run -d -p 7101:7101 --rm cordproj/cord-broker:0

**Cargo**

    $ cargo install cord-broker
    $ cord-broker &

Next, use the [Cord Client](https://github.com/cord-proj/cord-client) to interact with
the Broker. You can implement Cord within your own project using the
Client library ([docs.rs](https://docs.rs/cord-client)), however the easiest way to get
started is by using the CLI.

Subscribe to a namespace:

**Docker**

    $ docker run --rm cordproj/cord-client:0 -a <broker_addr> sub /names

**Cargo**

    $ cargo install cord-client
    $ cord-client sub /namespaces

Publish to this namespace:

**Docker**

    $ docker run -it --rm cordproj/cord-client:0 -a <broker_addr> pub /names
    Start typing to create an event, then press enter to send it to the broker.
    Use the format: NAMESPACE=VALUE

    /names/first=Daz

**Cargo**

    $ cord-client pub /names
    Start typing to create an event, then press enter to send it to the broker.
    Use the format: NAMESPACE=VALUE

    /names/first=Daz

## Etymology

Cord derives its name from the _spinal cord_. The long term goal of this project is to
aggregate data from every part of your environment, so that the decisions you make within
that environment are better informed. This is akin to the central nervous system, which
uses the spinal cord to aggregate electrical feedback from nerve endings.
