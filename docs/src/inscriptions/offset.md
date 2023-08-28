Offset
======

In order to make an inscription on a sat other than the first, an offset can be
provided with tag `2`, causing the inscription to be made on the sat at the
given offset. If the offset is equal to or greater than the number of sats in
the input, it is ignored, and the inscription is made on the first sat as
usual. The value of the offset tag is the little endian offset, with trailing
zeros omitted.

This allows creating multiple inscriptions in a single transaction, which
otherwise would all be made on the same sat.

An even tag is used, so that old versions of `ord` consider the inscription to
be unbound, instead of assigning it, incorrectly, to the first sat.

### Examples

An inscription at offset 255:

```
OP_FALSE
OP_IF
  OP_PUSH "ord"
  OP_PUSH 1
  OP_PUSH "text/plain;charset=utf-8"
  OP_PUSH 2
  OP_PUSH 0xff
  OP_PUSH 0
  OP_PUSH "Hello, world!"
OP_ENDIF
```

An inscription at offset 256:

```
OP_FALSE
OP_IF
  OP_PUSH "ord"
  OP_PUSH 1
  OP_PUSH "text/plain;charset=utf-8"
  OP_PUSH 2
  OP_PUSH 0x0001
  OP_PUSH 0
  OP_PUSH "Hello, world!"
OP_ENDIF
```
