# ToolkitAPI — Go SDK

[![Go Reference](https://pkg.go.dev/badge/github.com/toolkitapi/go-sdk.svg)](https://pkg.go.dev/github.com/toolkitapi/go-sdk)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Official Go SDK for [ToolkitAPI.io](https://toolkitapi.io) — a family of focused
HTTP APIs covering DNS, email, images, PDFs, scraping, AI-powered text tools,
barcodes, media extraction, webhooks, and more.

## Installation

```bash
go get github.com/toolkitapi/go-sdk
```

Requires Go **1.21+**.

## Quick start

```go
package main

import (
	"fmt"
	toolkitapi "github.com/toolkitapi/go-sdk"
)

func main() {
	client := toolkitapi.NewClient("https://toolkitapi.io", "tk_live_...")

	// DNS lookup
	result, err := client.Dns.Lookup(map[string]interface{}{
		"domain": "example.com",
	})
	if err != nil {
		panic(err)
	}
	fmt.Println(result)

	// Readability analysis
	score, err := client.Textanalysis.Readability(map[string]interface{}{
		"text": "The quick brown fox jumps over the lazy dog.",
	})
	if err != nil {
		panic(err)
	}
	fmt.Println(score)
}
```

## Toolkits

| Field | Highlights |
| --- | --- |
| `Analytics` | Query CSV/JSON/Parquet data with natural language |
| `Auth` | JWT create/decode, TOTP, OAuth helpers, API-key generation |
| `Barcode` | Barcode and QR code generation and decoding |
| `Convert` | Format (JSON/YAML/CSV/XML) and unit conversions |
| `Devtools` | JSON/YAML/XML validators, regex tester, UUID, hashing, fake data |
| `Dns` | DNS records, WHOIS, propagation, email auth, typosquat, SSL certs |
| `Email` | Validation, deliverability, disposable detection, SPF/DMARC |
| `Geo` | IP geolocation, reverse geocoding, distance/bearing, timezone |
| `Image` | Resize, convert, optimise, analyse, remove background |
| `Media` | YouTube metadata/transcripts, universal media extraction |
| `Pdf` | Generate, merge, split, extract, stamp, protect |
| `Scrape` | Web scraping, readability, meta, SEO audits, broken-link checks |
| `Textanalysis` | Readability, PII masking, profanity, similarity, summarize, language |
| `Webhook` | Request bins, HTTP mocks, replay captured requests |

Full endpoint reference at <https://toolkitapi.io/docs>.

## Authentication

Every request is authenticated via the `X-API-Key` header. Pass your key as
the second argument to `NewClient`.

Get your API key at <https://toolkitapi.io/account/signup>.

## Error handling

All toolkit methods return an `(interface{}, error)` pair. Network errors and
non-2xx HTTP responses are returned as the `error` value.

```go
result, err := client.Dns.Lookup(map[string]interface{}{
    "domain": "example.com",
})
if err != nil {
    log.Fatalf("lookup failed: %v", err)
}
```

## License

MIT
