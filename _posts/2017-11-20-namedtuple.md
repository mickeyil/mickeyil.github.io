---
layout: post
title: "Named Tuple"
description: ""
category: 
tags: [code, python]
---

I've recently been into the task of a module rewrite. This module has several methods which pass a rectangular regoin of interest from one place to another. Back then when I wrote it, the first thought was to pass the ROIs as tuples containing (x, y, width, height), but that was dismissed in favour of dictionary because it was much more readable:

The tuple way:
```python
  # tuple representing the rectangle
  # difficult to determine by glancing what the region of interest looks like 
  roi = (150, 100, 100, 200)
  
  # ...
  if roi[0] + roi[2] > image_width:
    raise ValueError('out of bounds')
```

With dictionary:
```python
  roi = dict(x=150, y=100, width=100, height=200)

  if roi['x'] + roi['width'] > image_width:
    raise ValueError('out of bounds')
```

Named tuple makes it even more clean. It can be used to build classes of objects that bundle up attributes together.

```python
  import collections

  # define a new tuple subclass named 'ROI' and assign it to the variable ROI
  ROI = collections.namedtuple('ROI', ('x', 'y', 'width', 'height'))

  # creation is clear like in a dictionary, with the advantage that named tuple
  # do not have per-instance dictionaries so the amount of memory the use is
  # the same as regular tuples.
  roi = ROI(x=150, y=100, width=100, height=200)

  if roi.x + roi.width > image_width:
    raise ValueError('out of bounds')
```

