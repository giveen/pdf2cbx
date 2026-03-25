# pdf2cbx

Convert PDFs into CBZ/CBR archives (comic book archives) using a small, portable
shell script. Designed to be simple, dependency-light and runnable without
installation.

Key features
- Convert PDF pages to JPEG images using `pdftocairo`.
- Package images into `CBZ` (zip) or `CBR` (rar) archives.
- Safe temporary-directory handling and absolute/relative input path support.

Quick start
1. Make the script executable and run from the folder where the script lives:

```bash
chmod +x pdf2cbx
./pdf2cbx -z -f /path/to/file.pdf    # create CBZ in current directory
```

2. (Optional) Install globally so you can run it from anywhere:

```bash
sudo mv pdf2cbx /usr/local/bin/pdf2cbx
sudo chmod +x /usr/local/bin/pdf2cbx
pdf2cbx -h
```

Requirements
- `pdftocairo` (poppler-utils) — used to rasterize PDF pages to JPEG.
- `zip` — used to create `.cbz` archives.
- `rar` — used to create `.cbr` archives.

Optional (image optimization)
- `jpegoptim` — recommended for lightweight JPEG optimization (lossy/lossless options).
- `mozjpeg` — optional, provides better compression but is slower.


Optimization
- Enable JPEG optimization with `-O` and set quality with `-q` (default 85). Example:

```bash
./pdf2cbx -O -q 85 -z -f mybook.pdf
```
If `jpegoptim` is installed it will be used; otherwise the script will fall back to `mozjpeg` (`cjpeg`) when available, or skip optimization with a warning.

Use `pdf2cbx -t` to test that required commands are available on the host.

Usage

```
pdf2cbx [options] <file>

Options:
  -f <file>    File to convert (or pass the file as a positional argument)
  -z           Create a CBZ archive (default)
  -r           Create a CBR archive
  -t           Test dependencies
  -v           Print version
  -h           Print help
```

Examples

- Create a CBZ from `mybook.pdf`:

```bash
./pdf2cbx -z -f mybook.pdf
```

- Create a CBR using positional argument:

```bash
./pdf2cbx -r mybook.pdf
```

Notes and troubleshooting
- The script creates a temporary working directory and removes it when done.
- Filenames with spaces should work, but quoting the path is recommended.
- If `pdftocairo` is missing, install it via your package manager (e.g. `sudo apt install poppler-utils`).

Contributing
- Small, focused patches welcome. Please open a PR against the `master` branch.

Acknowledgements
- Original project by Mickaël J and contributions from the community.

