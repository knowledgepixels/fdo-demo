# FDO Demo

### Basis

- [FDO Framework Ontology](https://w3id.org/fdof/ontology)
- [Nanopublications](https://nanopub.net/)

### Examples

- [FIP matrix](https://w3id.org/np/RA_03LCp_LLNR-3eGEIttU0LL5PqkgJRCA4dqN__mY-bs)

### Protocol

Getting object:

    $ curl -L -H 'FDO: object' https://w3id.org/np/RA_03LCp_LLNR-3eGEIttU0LL5PqkgJRCA4dqN__mY-bs

Getting metadata record:

    $ curl -L -H 'FDO: record' -H 'Accept: application/ld+json' https://w3id.org/np/RA_03LCp_LLNR-3eGEIttU0LL5PqkgJRCA4dqN__mY-bs

### Principles

- Open standards (HTTP, RDF, SPARQL)
- No lock-in (Open Source software, open ecosystem, "run it yourself" option)
- Designed for scalability (distribution, decentralization, data partitioning)
