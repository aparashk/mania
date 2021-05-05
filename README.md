# Mania 👻

Mania is a command-line tool for downloading music from [TIDAL](https://tidal.com). It is intended for educational and private use only, and **not** as a tool for pirating and distributing music.

## Installation

```
pip3 install --user --upgrade "https://github.com/evan-goode/mania/archive/master.zip"
```

Mania requires Python 3.6 or higher and has been tested on GNU/Linux and macOS.

## Usage

Instead of asking for your username and password, Mania now uses TIDAL's TV login process. The first time you run it, it will ask you to link a TIDAL account. Simply follow the link it gives you and log in.

To download a track, an album, or even an artist's entire discography:

```
mania track the great gig in the sky
mania album the dark side of the moon
mania artist pink floyd
```

To include EPs and singles in the discography:

```
mania artist pink floyd --include-eps-singles
```

You can also give it a URL to something in the TIDAL catalog and Mania will try to parse it:

```
mania url https://tidal.com/browse/track/140538043
```

Optional flags can go anywhere in the command. For example, to automatically select the top search result:

```
mania track the great gig in the sky --lucky
```

## Configuration

Each option (except `--config-file`) can be specified either as a command-line argument or using the TOML config file at `~/.config/mania/config.toml`. On the command line, prefix the option with `--`, or `--no-`, as in `--output-directory ~/music` or `--no-full-structure`.

The first time it's run, Mania populates `~/.config/mania/config.toml` with some default values. For more information on the TOML format, see https://github.com/toml-lang/toml.

To point Mania to a different configuration file, use `--config-file <file>`.

Available options are:

- `quality <quality>`: default value is `lossless`. Possible values are `master` (MQA in a FLAC container, usually 96 kHz, 24 bit), `lossless` (44.1 kHz, 16 bit FLAC), `high` (~320 kbps VBR AAC), and `low` (~96 kbps VBR AAC). If the content you request isn't available in the specified quality, Mania will try to download the "next best" option (`master` > `lossless` > `high` > `low`). Note that `master` and `lossless` require a TIDAL HiFi subscription.
- `output-directory <path>`: where to put downloaded music. Default value is `.` (your working directory when you run Mania).
- `by-id`: find something using its ID instead of searching TIDAL. For example, `mania album --by-id 79419393`.
- `lucky`: automatically download the top search result. Default value is `false`.
- `search-count <number>`: how many results to include in the search. Default value is `16`.
- `quiet`: don't log any output. Default value is `false`.
- `nice-format`: rename downloaded material to follow kebab-case and strip out special characters. "Maxwell's Silver Hammer (Remastered).mp3" becomes "maxwells-silver-hammer-remastered.mp3". Default value is `false`.
- `full-structure`: always organize content by artist and album. For example, `mania track --full-structure --lucky "isn't she lovely"` would create `Stevie Wonder/Songs In The Key Of Life/Disc 2/01 Isn't She Lovely.flac`. Default value is `false`.
- `skip-metadata`: don't download cover art or set tags. Not sure why someone would want this. Overrides `replay-gain`. Default value is `false`.
- `replay-gain`: tag FLAC files with [ReplayGain](https://en.wikipedia.org/wiki/ReplayGain) data from TIDAL (for normalization). Overridden by `skip-metadata`. Default value is `true`.
- `include-eps-singles`: include EPs and singles when downloading discographies with `mania artist`. Default value is `false`; prolific artists can have a _lot_ of singles/remixes and often you just want the studio albums.

## License

[The Unlicense](https://unlicense.org)

## See also

- [tidalapi](https://github.com/tamland/python-tidal)
- [RedSea](https://github.com/Dniel97/RedSea)
- [Tidal-Media-Downloader](https://github.com/yaronzz/Tidal-Media-Downloader/)
