### Summary

converting ODD to HTML doc: doc shows incorrect relationships for elements outside the TEI namespace

### Versions

OS: Debian testing (up to date as of 2013-12-27)

Reproducible with:

- tei-xsl 7.6.0

- github repository at commit 37919b645d5e33d1e7bc8e071ad3da8e726fdc98

### How to Reproduce

1. Clone or otherwise download the file tree at: https://github.com/lddubeau/teibugs/teibug33

2. In the directory ``teibug33``, issue:

    $ roma2 --doc --dochtml --nodtd --noxsd myTEI.xml out

(You can use ``--tei=...`` if you want to reproduce against a checked out version of the github repository.)

### Actual Results

The documentation shows that element ``flerbl`` in the ``http://foo.foo/foo`` namespace is:

* Contained by "empty element".

And that the element ``cit`` in the ``http://foo.foo/foo`` namespace:

* May contain "empty element".

* Has a declaration ``element cit { foo_flerbl }``, without links to ``foo_flerbl``.

### Expected Results

The element ``flerbl`` in the ``http://foo.foo/foo`` namespace should be documented to:

* Be contained by the element ``cit`` in the ``http://foo.foo/foo`` namespace.

The element ``cit`` in the ``http://foo.foo/foo`` namespace should be documented to:

* Contain the element ``flerbl`` in the ``http://foo.foo/foo`` namespace.

* Have a declaration ``element cit { foo_flerbl }``, which links to ``foo_flerbl``, just like all the elements in the TEI namespace have links in their declarations.
