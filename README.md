# FDO Demo

### Technical Basis

- [FDO Framework](https://fairdigitalobjectframework.org/) ([ontology](https://w3id.org/fdof/ontology))
- [Nanopublications](https://nanopub.net/)
- [Nanopublication Server Network](https://monitor.knowledgepixels.com/)

### Principles

- Open standards (HTTP, RDF, SPARQL)
- No lock-in (Open Source software, open ecosystem, "run it yourself" option)
- Designed for scalability (distribution, decentralization, data replication/partitioning)
- Flexibility / freedom (free choice of: identifier schemes, domain vocabularies, servers, data storage locations)
- Fast prototyping (learning while doing; ecosystem is up and running, ready to be used, and will keep evolving)

### Examples

FIP matrix:
- FDO ID/URL: https://w3id.org/np/RA1sDguLHiK1VcRs_kHLCE0IxdIIwihrn8WTxehuzcaAg#fip-matrix (we can later also use nicer URLs like `https://example.org/fdo4de/fip-matrix`)
- Metadata record (nanopublication) ID/URL: https://w3id.org/np/RA1sDguLHiK1VcRs_kHLCE0IxdIIwihrn8WTxehuzcaAg
- Digital Object file (bit sequence): https://raw.githubusercontent.com/peta-pico/dsw-nanopub-api/873763c608a0559d4ebc5e070c7ef555b2de9e6d/tables/new_matrix.csv (this file can live side by side with the nanopublication, or on a different server/system; can be open or have restricted access with required authentication)

More examples in [fdo-examples](https://github.com/knowledgepixels/fdo-demo/tree/main/fdo-examples).

### Creating FDOs

- [Template for manual creation](https://nanodash.knowledgepixels.com/publish?252&template=https://w3id.org/np/RADQPVz2_GAPjL6tU8PiA010UNnsi7sjEEOOHLETgyzi8&template-version=latest) (with Nanodash)
- Libraries and command-line tools ([nanopub-java](https://github.com/Nanopublication/nanopub-java), [nanopub-rs](https://vemonet.github.io/nanopub-rs/)) can be used for automatic creation

### Protocol

HTTP with new header field `FDO`:

- `FDO: record` returns the metadata record for the given FDO (default)
- `FDO: object` returns the actual object (dataset, picture, etc.)

Using `curl` to get FDO metadata record (as nanopublication):

    $ curl -L -H 'FDO: record' -H 'Accept: application/ld+json' https://w3id.org/np/RA_03LCp_LLNR-3eGEIttU0LL5PqkgJRCA4dqN__mY-bs

Using `curl` to get FDO object:

    $ curl -L -H 'FDO: object' https://w3id.org/np/RA_03LCp_LLNR-3eGEIttU0LL5PqkgJRCA4dqN__mY-bs

This is compliant with the FDO Framework specification (see above), with some small suggestions for improvement, which we will discuss with the FDO community.

### Querying

Query to get FDOs:

- [Simple client to API](https://tapas.knowledgepixels.com/tapas.html?api=RAZgtM7Kzb0aTBlH4coOzlfgzBOoofqROCIMZTW3KliLQ&op=/get-fdos)
- Same on the command line: `$ curl -L 'https://query.knowledgepixels.com/api/RAZgtM7Kzb0aTBlH4coOzlfgzBOoofqROCIMZTW3KliLQ/get-fdos?query=matrix'`
- [Custom SPARQL query](https://query.knowledgepixels.com/tools/full/yasgui.html#query=prefix+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0Aprefix+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0Aprefix+np%3A+%3Chttp%3A%2F%2Fwww.nanopub.org%2Fnschema%23%3E%0Aprefix+npa%3A+%3Chttp%3A%2F%2Fpurl.org%2Fnanopub%2Fadmin%2F%3E%0Aprefix+npx%3A+%3Chttp%3A%2F%2Fpurl.org%2Fnanopub%2Fx%2F%3E%0Aprefix+xsd%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0Aprefix+dct%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0Aprefix+fdof%3A+%3Chttps%3A%2F%2Fw3id.org%2Ffdof%2Fontology%23%3E%0A%0Aselect+%3Ffdo+%3Ftype+%3Fnp+%3Fcreator+where+%7B%0A++graph+npa%3Agraph+%7B%0A++++%3Fnp+npx%3AhasNanopubType+fdof%3AFAIRDigitalObject+.%0A++++%3Fnp+dct%3Acreator+%3Fcreator+.%0A++++%3Fnp+npa%3AhasValidSignatureForPublicKey+%3Fpubkey+.%0A++++filter+not+exists+%7B+%3Fnpx+npx%3Ainvalidates+%3Fnp+%3B+npa%3AhasValidSignatureForPublicKey+%3Fpubkey+.+%7D%0A++++%3Fnp+np%3AhasAssertion+%3Fa+.%0A++%7D%0A++graph+%3Fa+%7B%0A++++%3Ffdo+fdof%3AhasInformationObjectType+%3Ftype+.%0A++%7D%0A%7D&contentTypeConstruct=text%2Fturtle&contentTypeSelect=application%2Fsparql-results%2Bjson&endpoint=%2Frepo%2Ffull&requestMethod=POST&tabTitle=Query&headers=%7B%7D&outputFormat=table)

### Type Registry

With nanopublications, the same system that is used to describe/register FDOs can also be used to describe/register FDO Types (and many other things).

- [Template to declare new FDO types](https://nanodash.knowledgepixels.com/publish?template=https://w3id.org/np/RAGgM9kYzzaGF9eY1eawXCG-U-_HOEdw6NOnghAb5ijZA&template-version=latest)
- [Example nanopublication declaring an FDO type](https://w3id.org/np/RAddkhsbvqc-VM_Y5t7uf_AD-WJbd7WybVmJdx7TPDV4o)

### Additional Metadata

TODO:

- Define new FDO type 'Table'
- Allow for additional metadata on rows (names, descriptions, concept IDs, ...)
- Query FDOs by table columns

### Distributed, Redundant, Scalable

Checking availability of a nanopublication (using [nanopub-java](https://github.com/Nanopublication/nanopub-java) as command-line tool):

    $ np status -a https://w3id.org/np/RA_03LCp_LLNR-3eGEIttU0LL5PqkgJRCA4dqN__mY-bs
    URL: https://np.knowledgepixels.com/RA_03LCp_LLNR-3eGEIttU0LL5PqkgJRCA4dqN__mY-bs
    URL: http://130.60.24.146:7880/RA_03LCp_LLNR-3eGEIttU0LL5PqkgJRCA4dqN__mY-bs
    URL: http://server.np.dumontierlab.com/RA_03LCp_LLNR-3eGEIttU0LL5PqkgJRCA4dqN__mY-bs
    URL: https://server.np.trustyuri.net/RA_03LCp_LLNR-3eGEIttU0LL5PqkgJRCA4dqN__mY-bs
    URL: http://server.nanopubs.lod.labs.vu.nl/RA_03LCp_LLNR-3eGEIttU0LL5PqkgJRCA4dqN__mY-bs
    URL: http://app.tkuhn.eculture.labs.vu.nl/nanopub-server-4/RA_03LCp_LLNR-3eGEIttU0LL5PqkgJRCA4dqN__mY-bs
    Found on 6 nanopub servers.

All APIs are distributed and redundant (and thereby scalable) too, for example:

    $ curl -L 'https://query.knowledgepixels.com/api/RAZgtM7Kzb0aTBlH4coOzlfgzBOoofqROCIMZTW3KliLQ/get-fdos?query=matrix'
    $ curl -L 'https://query.np.trustyuri.net/api/RAZgtM7Kzb0aTBlH4coOzlfgzBOoofqROCIMZTW3KliLQ/get-fdos?query=matrix'
    $ curl -L 'https://query.np.kpxl.org/api/RAZgtM7Kzb0aTBlH4coOzlfgzBOoofqROCIMZTW3KliLQ/get-fdos?query=matrix'

See the [monitor](https://monitor.knowledgepixels.com/) for the current network of services.
