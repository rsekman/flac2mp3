# flac2mp3

Shell script to encode FLAC to mp3 while keeping tags

Dependencies: `metaflac flac lame sed` and any UNIX shell.

# Usage

```bash
FLACOPTS=<options for flac> # default: -s
LAMEOPTS=<options for LAME> # default: --vbr-new -V 0 --quiet
flac2mp3 <in.flac> <out.mp3>
```

# Details

Tags are preserved by reading the metadata with `metaflac` and using `sed` to substitute ID3v2.3 fields for the `metaflac` tag names.
Additional tags can be supported by adding more patterns like
```bash
s/^[metaflac tag name]=/[ID3v2.3 field]=/p
s/^[metaflac tag name]=/TXXX=[description]=/p
```
The former applies for [frames described in the ID3v2.3 specification](https://id3.org/id3v2.3.0#Declared_ID3v2_frames), and the latter for user-defined frames (e.g., MusicBrainz metadata).
