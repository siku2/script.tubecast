---
title: Command Message Format
---



YouTube uses Google's [Channel API]() for communication between the client and the host.
See [gvsumasl/jacc](https://github.com/gvsumasl/jacc) for an implementation of the protocol.

Here's an overview:

## Format



### Chunk

A chunk contains one or multiple messages.
The chunk data itself is a valid JSON array but each chunk is prefixed by the length of the data.

#### Message

Each message is an entry in the chunk's message JSON arraz.

A message consists of two parts. The message code and the payload.

The code is a unique number assigned to each message. It can be used to avoid handling the same message multiple times. It seems to be an incrementing number so a simple anti-duplicate implementation is to check whether the current message code is bigger than the previous one.

In YouTube's case the payload is always a JSON array starting with the operation code (a string) and followed by the arguments (optional).

## Example

```
+=================================================================================+
|                                      CHUNK                                      |
+------+--------------------------------------------------------------------------+
| SIZE |                                 MESSAGES                                 |
+------+-+-------------------+---+-----------------------+---+---------------+----+
|      | |         1         |   |           2           |   |       3       |    |
+------+-+-------------------+---+-----------------------+---+---------------+----+
| 71\n  [[7,["getNowPlaying"]]\n,[8,["getSubtitlesTrack"]]\n,[9,["getVolume"]]\n] |
+=================================================================================+
```
