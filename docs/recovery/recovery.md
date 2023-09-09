Manual file recovery via TUUP should be done in a manner that is possible without third-party protocols or networks, including the Internet. It should be able to be done with analog tools in as simple a way as possible - while
remaining concise and efficient. This method is free to be updated and standardized within the TUUP community, but legacy recovery methods should always remain able to be used so long as the protocol may allow for it. Networks 
run outside of the realm of the general community may accelerate development (or stay behind), and may employ their own recovery methods that won't work within the community-updated methods. This is fine, as anyone running
such networks already assume their own responsibilities; they cannot receive community support after Layer 1.

## A Quick Rundown on Terminology

We should first clarify the layers of TUUP.

- Layer 0: The Concept.
- Layer 1: The Protocol.
- Layer 2: The Network.
- Layer 3: The Application.

When discussing recovery, we're discussing the retrieval of data from a network running via TUUP. TUUP allows for data to be redundantly distributed amonst nodes running on-chain. Under the current version, the following should be noted:

- Data is striped over multiple nodes.
- A section of the block stripe is called a "_chunk_".
- Each chunk is shifted `+1` for every _n_ node.
- Chunk shifts are represented by _Δ_.
- Each stripe is given an identifier value, called an _eigenseed_ (name to be changed in the future).
- Eigenseeds are represented as an integer sub λ, represented in common text as `λ_{<eigenseed>}`.
- If all chunks match in a valid stripe, the output will be raw data in binary format, with a signal marked `TRUE`.
- Maximum lower bound for λ<sub>(m)</sub> is λ<sub>2</sub>, with no maximum upper bound.
- Stripe and chunk sizes are provably irregular. While the minimum size will be at least one bit, there is no byte limit per completed stripe.
- Stripe chunks are generically identified algebraically as _K_, with an identifying integer sub, represented in common text as `K_{<integer>}`.
- Chunk bounds are limited by byte size.
- Storage upper bounds will be represented as _p_, and storage lower bounds will be represented as _q_.
- Duplicate values may be found in completely different chunks.
- A minimum chunk value is one byte. If a distributed number of chunk values result in an odd number, a placeholder "`NULL`" byte will tail the remainder byte.

Given the following in binary:
```
01100100
01110010
00101110
00100000
01100011
01100001
01110100
```
We can make the following representations:
```
01100100  A
01110010
00101110  B
00100000
01100011  C
01100001
01110100  D
00000000
```
A common four-node network may look like this:

| FLANDRE | CIRNO | ALICE |
| ------- | ----- | ----- |
| A<sub>0</sub> B<sub>0</sub> C<sub>0</sub> D<sub>0</sub> | D<sub>0</sub> A<sub>0</sub> B<sub>0</sub> C<sub>0</sub> | C<sub>2</sub> D<sub>2</sub> A<sub>2</sub> B<sub>2</sub> | 
| B<sub>1</sub> C<sub>1</sub> D<sub>1</sub> A<sub>1</sub> | C<sub>1</sub> D<sub>1</sub> A<sub>1</sub> B<sub>1</sub> | B<sub>2</sub> C<sub>2</sub> D<sub>2</sub> A<sub>2</sub> |
| C<sub>2</sub> D<sub>2</sub> A<sub>2</sub> B<sub>2</sub> | B<sub>2</sub> C<sub>2</sub> D<sub>2</sub> A<sub>2</sub> | A<sub>2</sub> B<sub>2</sub> C<sub>2</sub> D<sub>2</sub> |
| D<sub>3</sub> A<sub>3</sub> B<sub>3</sub> C<sub>3</sub> | A<sub>2</sub> B<sub>2</sub> C<sub>2</sub> D<sub>2</sub> | D<sub>2</sub> A<sub>2</sub> B<sub>2</sub> C<sub>2</sub> |

To represent the stripes, we use our common formatting scheme:

_(*) optional_

`<(*)COMMUNITY><NETWORK><NODE>λ_{<eigenseed>}`

To identify a stripe in our example above, we use the following method:

**EXAMPLE_NETWORK** FLANDRE λ<sub>(0)</sub>

To identify a range of stripes, we would do the following:

**EXAMPLE_NETWORK** FLANDRE λ<sub>(0⋯3)</sub>

In a recovery method, one would first identify chunks by their common shifted value per the number of users within a network. They would then determine an eigenseed range, then - in order from λ<sub>(2)</sub> of all known nodes - list
known eigenseeds of the range. From there, you begin the reverse shift - K<sub>-Δ</sub>. The reverse shift from the automatic known node range will automatically give the user the stripes, and they will automatically know the sizes of
the bytes, as well as the final output - in binary.

## Things Left To-Do

- An actual formula for what is described above should be made in the name of being concise.
- A different name should be had for what we represent as an "eigenseed", as to not confuse it with linear algebra.
