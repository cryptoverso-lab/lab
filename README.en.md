# lab.cryptoverso.net — the book's routes

*Leggi in [italiano](README.md).*

This repository serves one host: **[lab.cryptoverso.net](https://lab.cryptoverso.net)**, the address printed next to every QR code in *La matematica di chi perde* by Luigi Garone.

It holds no content. It holds **routes**: one folder per printed code, each containing a page that forwards to the matching notebook.

```
lab.cryptoverso.net/l01    →   Lab 1 on Google Colab
lab.cryptoverso.net/c01    →   Calculator 1 on Google Colab
lab.cryptoverso.net/codice →   the code repository
lab.cryptoverso.net/errata →   errors found after printing
```

## Why it exists

A printed QR code cannot be fixed. If the book's codes pointed straight at GitHub or Colab, the day either service changes an address — or the day the code moves to a different organisation — every copy already in print would become a dead end.

Pointing at a host we control means **the destination stays editable forever**: change one line here and the QR codes already on paper keep working. It is the same reason DOIs exist.

Hence one rule, with no exceptions:

> **Routes are never renamed and never deleted.** A code published on paper is a permanent commitment. If a destination dies, the route gets repointed — not removed.

## How it is updated

These pages are **not written by hand**. They are generated from the book's production repository, where the list of routes lives alongside the chapters that cite them:

```bash
uv run python codice/figure/genera_redirect.py --sito
```

That command rewrites the pages, the `CNAME` file and the index, all from the same source the printed QR codes come from. The result is then published here. Editing a page directly in this repository creates a gap between what is printed and what is served: at the next generation the edit disappears, and nobody remembers why it was there.

The generator also carries a safety gate: it **refuses to produce QR codes for a domain that does not resolve in DNS**. A QR printed against a name that does not exist is the most expensive mistake in the whole production, because you only find out once the book is bound.

## What a route looks like

One page, no JavaScript, no dependencies:

- a `<meta http-equiv="refresh">` that forwards immediately;
- a `<link rel="canonical">` to the same destination, so search engines index the notebook rather than the route;
- a visible link, for readers with auto-forwarding disabled or on a slow connection.

The forward is stated in plain sight: you see where you are going before you get there.

## Infrastructure

Served by **GitHub Pages** on a custom domain: the `CNAME` file declares `lab.cryptoverso.net`, and the subdomain's DNS record is a CNAME to `cryptoverso-lab.github.io`. The `.nojekyll` file stops Jekyll from skipping paths that begin with an underscore.

## Where everything else lives

The book's code — computation engine, notebooks, frozen data, figure generators — is in **[cryptoverso-lab/matematica-di-chi-perde](https://github.com/cryptoverso-lab/matematica-di-chi-perde)**, together with the generator of these pages.

## Licence

MIT, same as the book's code.

---

<div align="center">

<br>

<img src="assets/cryptoverso-logo.svg" alt="Cryptoverso" width="56">

**Luigi Garone — [Cryptoverso](https://cryptoverso.net)**

</div>
