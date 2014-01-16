### Summary

ODD: the resolution of unprefixed names in ``<rng:ref>`` has changed

### Versions

OS: Debian testing (up to date as of 2014-01-16)

tei-xsl: see below

### How to Reproduce

1. Clone or otherwise download the file tree at: https://github.com/lddubeau/teibugs/tree/master/teibug34

2. Install tei-xsl 7.6.0.

3. In the directory ``teibug34``, issue:

        $ roma --nodtd --noxsd myTEI.xml out_7.6.0

4. Install tei-xsl 7.8.0.

5. In the directory ``teibug34``, issue:

        $ roma --nodtd --noxsd myTEI.xml out_7.8.0

6. Run:

        $ diff -u out_7.6.0/foo.rnc out_7.8.0/foo.rnc

### Actual Results

The output of the diff (abbreviated to remove the timestamp difference) looks like this:

```
--- out_7.6.0/foo.rnc   2014-01-16 12:52:02.626985982 -0500
+++ out_7.8.0/foo.rnc   2014-01-16 12:52:27.734940939 -0500
@@ -4227,9 +4227,5 @@
 foo_a =

   ##
-  element ns2:a { foo_b }
-foo_b =
-
-  ##
-  element ns2:b { text }
+  element ns2:a { empty }
 start = tei_TEI
```

### Expected Results

No difference in the expected structure of the XML document which ``foo.rnc`` would validate.

### Observations

It seems in earlier versions roma would resolve ``<rng:ref name="b"/>`` by looking for unprefixed names and then looking for a prefix which without the prefix would be named ``"b"``. And now it does not do that.

At any rate, the net result is that an ODD which inadvertently hit on the earlier behavior will, from at least tei-xsl 7.8.0 onwards, generate a different schema.
