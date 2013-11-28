### Summary

odd2html.xsl: incorrect output if elements in two different namespaces have the same local-name()

### Versions

OS: Ubuntu 13.10

tei-p5-xsl2 6.34

### How to Reproduce

1. Clone or otherwise download the file tree at: https://github.com/lddubeau/teibugs/teibug32

2. In the directory ``teibug32``, issue:

    $ roma2 --doc --dochtml --nodtd --noxsd myTEI.xml out

### Actual Results

The file ``out/foo.doc.html`` does not allow to distinguish on the basis of a simple HTML link the documentation for TEI's ``cit`` from the documentation for the new element ``cit`` in the namespace ``http://foo.foo/foo`` (henceforth referred with the ``foo:`` prefix). The documentation fragments for each of these two element are given the same HTML id: "cit".

Note that in effect this makes some of the documentation incorrect because when a content model means to link to ``foo:cit``, the browser brings the user to TEI's ``cit`` element instead.

### Expected Results

A structure that allows distinguishing ``foo:cit`` from TEI's ``cit`` using simple HTML links.
