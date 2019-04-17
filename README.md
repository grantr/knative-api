# Knative API repository demo

This is a demo of what a Knative API repository would look like if it followed
the pattern of https://github.com/kubernetes/api.

**THIS REPOSITORY IS JUST A DEMO. IT DOESN'T ACTUALLY WORK.**

### Why is the api machinery code in here?

https://github.com/knative/pkg includes a bunch of api machinery code,
equivalent to https://github.com/kubernetes/apimachinery. Should that be here or
in its own repository?

### Where are the client libraries?

Client libraries are not included here for the following reasons:

* **An API repository should change only when the APIs change.** Including
  the Go client here would require a new version to be cut when the Go
  client implementation changes, even if the API definition didn't change.
* **API definitions may be used by clients in multiple languages.** A client
  written in Python doesn't care about changes to Golang clients. Including
  the Go client here forces the Python developer to track those changes
  anyway.
* **Dependencies should be the minimum needed to specify the APIs.**
  Because this repository will be imported by many projects, its dependencies
  should be minimal to avoid conflicts.

Generated clients can be provided in a different repository, similar to
https://github.com/kubernetes/client-go.

### Ok, so why are Go types here at all versus Protobuf definitions?

We expect that most implementations of these types will be written in Go.
Including Go types seems like the right compromise between annoying Go
developers and annoying other developers.

Ultimately this repository should include both Go types and generated Protobuf
definitions, similar to https://github.com/kubernetes/api.
