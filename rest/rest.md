#REST Introduction

REST stands for [Representational state transfer][1] and is one of the most common client/server architectures in use today on the internet. You can read more about the details in the excellent Wikipedia article referenced in the previous sentence.  MaaSive.net APIs use the following five REST methods:

- [OPTIONS][] &mdash; info about the current uri
- [GET][] &mdash; read/find
- [POST][POST_PUT] &mdash; create
- [PUT][POST_PUT] &mdash; update
- [DELETE][] &mdash; delete

REST methods are really just HTTP verbs.  You can read all about them [here][http-verbs]

[1]: http://en.wikipedia.org/wiki/Representational_state_transfer
[OPTIONS]: #/docs/rest/options.md
[GET]: #/docs/rest/get.md
[POST_PUT]: #/docs/rest/post_put.md
[DELETE]: #/docs/rest/delete.md
[http-verbs]: http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods
