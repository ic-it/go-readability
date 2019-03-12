# Go-Readability

[![GoDoc](https://godoc.org/github.com/importcjj/go-readability?status.png)](https://godoc.org/github.com/importcjj/go-readability)
[![Travis CI](https://travis-ci.org/importcjj/go-readability.svg?branch=master)](https://travis-ci.org/importcjj/go-readability)
[![Go Report Card](https://goreportcard.com/badge/github.com/importcjj/go-readability)](https://goreportcard.com/report/github.com/importcjj/go-readability)

Go-Readability is a Go package that cleans a HTML page from clutter like buttons, ads and background images, and changes the page's text size, contrast and layout for better readability.

This package is fork from [readability](https://github.com/ying32/readability) and [go-readability](https://github.com/go-shiori/go-readability), which inspired by [readability for node.js](https://github.com/luin/readability) and [readability for python](https://github.com/kingwkb/readability).

## Why fork ?

There are severals reasons as to why I create a new fork instead sending a PR to original repository. Cause I need: 

- Extract images
- Readable mix HTML tags
- Custom line break

## Example

```Go  
package main

import (
	"fmt"
	nurl "net/url"
	"time"

	"github.com/importcjj/go-readability"
)

func main() {
	// Create URL
	url := "https://www.nytimes.com/2018/01/21/technology/inside-amazon-go-a-store-of-the-future.html"
	parsedURL, _ := nurl.Parse(url)

	extractor := &readability.Extractor{
		TextLineBreak:  "<br/><br/>",
		TextWithImgTag: true,
	}

	// Fetch readable content
	article, err := extractor.FromURL(parsedURL, 5*time.Second)
	if err != nil {
		panic(err)
	}

	// Show results
	fmt.Println(article.Meta.Title)
	fmt.Println(article.Meta.Excerpt)
	fmt.Println(article.Meta.Author)
	// readable content
	fmt.Println(article.Text)
	// Tidy HTML
	fmt.Println(article.HTML)
	// Images
	fmt.Println(article.Images)
}
```
