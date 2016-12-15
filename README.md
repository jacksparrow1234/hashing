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
