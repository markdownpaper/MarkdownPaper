## How to make a scientific looking PDF from markdown (with bibliography)

Markdown is the most common format for writing on GitHub, and is what I use for all of my own documentation. It also exports to HTML and other convenient formats for reading on mobile devices. However, sometimes you want to export it as a PDF so that you can author scientific papers and export the formats that pre-print servers like [arxiv.org](https://arxiv.org/) will accept.

![markdown example](https://gist.githubusercontent.com/maxogden/97190db73ac19fc6c1d9beee1a6e4fc8/raw/c127b99eddbd3491114aefaaa60a124e566d77a5/markdown.png)

The above example is from the [Dat Paper](https://github.com/datproject/docs/tree/master/papers).

### 1. Install Pandoc

[Pandoc](https://en.wikipedia.org/wiki/Pandoc) is a great tool for converting between different print formats. In this case pandoc will handle these conversions for us, all in one command:

```
Markdown -> Latex -> Latex Citeproc Bibliography Filter -> PDF
```

To install it on Mac OS using homebrew:

```
brew install pandoc pandoc-citeproc
```

### 2. Author your paper

See `paper.md` for an example. You can use YAML frontmatter to specify variables that Pandoc will use as the variables in it's Latex template. To see the Latex template you can run `pandoc -D latex`.

### 3. Create a bibliography

The `pandoc-citeproc` filter will automatically generate a references section for you at the end of your document, and also replace all Markdown references an academic citation style.

First you can grab some Bibtex references from Google Scholar and throw them in a `paper.bib` file:

![](https://gist.github.com/maxogden/97190db73ac19fc6c1d9beee1a6e4fc8/raw/adaaa9b5c19460d3be42021ef0c1b8e11a8d38fe/bibtex.png)

Then when you render the paper references will get converted automatically if you cite them using the identifier from the bibtex in Markdown like this:

```
The seminal work [@pizza2000identification]
```

### 4. Render it

Once you have `.md` and `.bib` files you can generate a PDF like this:

```
pandoc --filter pandoc-citeproc --bibliography=paper.bib --variable classoption=twocolumn --variable papersize=a4paper -s paper.md -o paper.pdf
```

Or generate the intermediate Latex source like this:

```
pandoc --filter pandoc-citeproc --bibliography=paper.bib --variable classoption=twocolumn --variable papersize=a4paper -s paper.md -t latex -o paper.txt
```

### 5. Upload it

Now you're ready to post the `.txt`, `.bib`, `.pdf` and `.md` files on a pre-print server, ideally with a CC0 public domain dedication license for maximum openness, and upload it to GitHub so others can access and re-use your research!
