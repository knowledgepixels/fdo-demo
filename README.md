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
- Nanopub ID/URL: https://w3id.org/np/RA1sDguLHiK1VcRs_kHLCE0IxdIIwihrn8WTxehuzcaAg
- Digital Object file (bit sequence): https://raw.githubusercontent.com/peta-pico/dsw-nanopub-api/873763c608a0559d4ebc5e070c7ef555b2de9e6d/tables/new_matrix.csv (this file can live side by side with the nanopublication, or on a different server/system; can be open or have restricted access with required authentication)

More examples in [fdo-examples](https://github.com/knowledgepixels/fdo-demo/tree/main/fdo-examples).

### Protocol

Getting object:

    $ curl -L -H 'FDO: object' https://w3id.org/np/RA_03LCp_LLNR-3eGEIttU0LL5PqkgJRCA4dqN__mY-bs

Getting metadata record:

    $ curl -L -H 'FDO: record' -H 'Accept: application/ld+json' https://w3id.org/np/RA_03LCp_LLNR-3eGEIttU0LL5PqkgJRCA4dqN__mY-bs

### Creating FDOs

- [Template for manual creation](https://nanodash.knowledgepixels.com/publish?252&template=https://w3id.org/np/RADQPVz2_GAPjL6tU8PiA010UNnsi7sjEEOOHLETgyzi8&template-version=latest)

### Querying

- [Query to get all FDOs](https://query.knowledgepixels.com/tools/full/yasgui.html#query=prefix+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0Aprefix+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0Aprefix+np%3A+%3Chttp%3A%2F%2Fwww.nanopub.org%2Fnschema%23%3E%0Aprefix+npa%3A+%3Chttp%3A%2F%2Fpurl.org%2Fnanopub%2Fadmin%2F%3E%0Aprefix+npx%3A+%3Chttp%3A%2F%2Fpurl.org%2Fnanopub%2Fx%2F%3E%0Aprefix+xsd%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E%0Aprefix+dct%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0Aprefix+fdof%3A+%3Chttps%3A%2F%2Fw3id.org%2Ffdof%2Fontology%23%3E%0A%0Aselect+%3Ffdo+%3Ftype+%3Fnp+%3Fcreator+where+%7B%0A++graph+npa%3Agraph+%7B%0A++++%3Fnp+npx%3AhasNanopubType+fdof%3AFAIRDigitalObject+.%0A++++%3Fnp+dct%3Acreator+%3Fcreator+.%0A++++%3Fnp+npa%3AhasValidSignatureForPublicKey+%3Fpubkey+.%0A++++filter+not+exists+%7B+%3Fnpx+npx%3Ainvalidates+%3Fnp+%3B+npa%3AhasValidSignatureForPublicKey+%3Fpubkey+.+%7D%0A++++%3Fnp+np%3AhasAssertion+%3Fa+.%0A++%7D%0A++graph+%3Fa+%7B%0A++++%3Ffdo+fdof%3AhasInformationObjectType+%3Ftype+.%0A++%7D%0A%7D&contentTypeConstruct=text%2Fturtle&contentTypeSelect=application%2Fsparql-results%2Bjson&endpoint=%2Frepo%2Ffull&requestMethod=POST&tabTitle=Query&headers=%7B%7D&outputFormat=table)
