# hashing


Please post here

Getting : 


Error
Traceback (most recent call last):
  File "/home/vimanyu/PycharmProjects/endterm/test.py", line 29, in test_hash
    self.assertEqual(self.node1, ring.hash(k))
  File "/home/vimanyu/PycharmProjects/endterm/hrw.py", line 64, in hash
    w = weight(n, key)
  File "/home/vimanyu/PycharmProjects/endterm/hrw.py", line 26, in weight
    node_hash = md5_hash(node)
  File "/home/vimanyu/PycharmProjects/endterm/hrw.py", line 15, in md5_hash
    return long(md5.md5(key).hexdigest(), 16)
TypeError: md5() argument 1 must be string or buffer, not int

=================

donot use ip2 long conversion.
just put the node direct in the weight function.



complete solution:---
==========================

__doc__ = """
Rendezvous hashing (Highest Random Weight hashing) implementation.
"""

import md5


def md5_hash(key):
    """Given a string key, return a long hash value."""
    return long(md5.md5(key).hexdigest(), 16)


def weight(node, key):
    """Return the weight for the key on node.
    @params:
        node : hostname or IP string to be hashed.
        key : string to be hashed.
    """
    a = 1103515245
    b = 12345
    node_hash = md5_hash(node)
    key_hash = md5_hash(key)
    return (a * ((a * node_hash + b) ^ key_hash) + b) % (2 ^ 31)


class Ring(object):
    """A ring of nodes supporting rendezvous hashing based node selection."""

    def __init__(self, nodes=None):
        nodes = nodes or {}
        self._nodes = set(nodes)

    def add(self, node):
        """Add the given node to the _nodes set."""
        self._nodes.add(node)

    def nodes(self):
        return self._nodes

    def remove(self, node):
        """Remove the given node from the _nodes set."""
        self._nodes.remove(node)

    def hash(self, key):
        """Return the node to which the given key hashes to."""
        assert len(self._nodes) > 0
        weights = []
        for node in self._nodes:
            w = weight(node, key)
            weights.append((w, node))
        _, node = max(weights)
        return node
