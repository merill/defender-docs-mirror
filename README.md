# Defender docs mirror

The Microsoft Defender, Microsoft Sentinel and Security Exposure Management
pages on Microsoft Learn, as Markdown, one file per page at the path of the
source file Learn built it from. It stands in for `MicrosoftDocs/defender-docs`,
which is no longer public: every commit here is a crawl that found something
new on Learn, so the history of this repository is the history of the
published docs.

- `learn-mirror.config.json` picks the sitemaps, TOCs and pages to mirror, and
  `sourceRepos` keeps out pages other repositories publish under the same
  Learn paths (`azure/`, for one).
- `.learn-mirror/state.json` records each page's ETag and the publish metadata
  stripped from its front matter, so a run only downloads pages that changed
  and a republish is not a diff.
- `.github/workflows/mirror-learn.yml` runs [learn-mirror](https://github.com/merill/learn-mirror)
  four times a day.

Content is © Microsoft, published on Microsoft Learn under
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
