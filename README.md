# cse2421tldr
Condensed notes on Ohio State CSE 2421 Spring 2021. https://bitblip.github.io/cse2421tldr/.

## Hugo
Markdown content is converted to a static website using [Hugo](https://gohugo.io/).

## Build
Content is deployed to GitHub pages using GitHub Actions workflow. see `.github/workflows/deploy.yml`

docker run -it --rm -p 1313:1313 -v $(pwd):/src klakegg/hugo:0.80.0 serve -D