# When the Music Stops: Tip-of-the-Tongue Retrieval for Music

This repository contains data collected in the paper 'When the Music Stops: Tip-of-the-Tongue Retrieval for Music'. To appear at SIGIR2023, [pre-print available on arXiv](https://arxiv.org/abs/2305.14072).

### Abstract

We present a study of Tip-of-the-tongue (ToT) retrieval for music, where a searcher is trying to find an existing music entity, but is unable to succeed as they cannot accurately recall important identifying information. ToT information needs are characterized by complexity, verbosity, uncertainty, and possible false memories. We make four contributions. (1) We collect a dataset—$`ToT_{Music}`$—of 2,278 information needs and ground truth answers. (2) We introduce a schema for these information needs and show that they often involve multiple modalities encompassing several Music IR sub-tasks such as lyric search, audio-based search, audio fingerprinting, and text search. (3) We underscore the difficulty of this task by benchmarking a standard text retrieval approach on this dataset. (4) We investigate the efficacy of query reformulations generated by a large language model (LLM), and show that they are not as effective as simply employing the entire information need as a query – leaving several open questions for future research.


### Authors
[Samarth Bhargav](https://samarthbhargav.github.io/) (work done during internship at Spotify Research), [Anne Schuth](https://anneschuth.nl/), [Claudia Hauff](https://chauff.github.io/)

### Cite
```
@inproceedings{bhargav2023,
  title = {When the Music Stops: Tip-of-the-Tongue Retrieval for Music},
  author = {Samarth Bhargav and Anne Schuth and Claudia Hauff},
  year = {2023},
  booktitle = {Proceedings of SIGIR'23},
  doi = {10.1145/3539618.3592086}
}
```

### Description

Data can be downloaded using [this link](data.jsonl.zip), which is a zipped JSONL file with one information need per line. You can view an example docuument [at the bottom of this Readme](#example-document). Each field and accompanying description is outlined in the table below:

| Field Name                                     | Type                | Description                                                                                                                                          |
|------------------------------------------------|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`                                           | Identifier (String) | Unique identifier                                                                                                                                    |
| `wasabi_2.0_id`                                | Identifier (String) | Corresponding item in the Wasabi 2.0 Corpus                                                                                                          |
| `wasabi_isrc`                                  | Identifier (String) | ISRC of the item, sourced from the Wasabi 2.0 Corpus                                                                                                 |
| `spotify_resolved`                             | Dict                | Denotes the matching Spotify song(s)                                                                                                                 |
| `spotify_resolved.title`                       | String              | Title of the song                                                                                                                                    |
| `spotify_resolved.items`                       | List (Dict)         | Associated Songs(s) on Spotify (multiple recordings can exists, any are considered relevant)                                                         |
| `spotify_resolved.items.IDX.url`               | URL                 | URL of song at index IDX                                                                                                                             |
| `spotify_resolved.items.IDX.isrc`              | List (String)       | ISRC(s)                                                                                                                                              |
| `spotify_resolved.items.IDX.album`             | List (Dict)         | Album song appears on                                                                                                                                |
| `spotify_resolved.items.IDX.album.name`        | String              | Album name                                                                                                                                           |
| `spotify_resolved.items.IDX.album.uri`         | URI                 | Album URI                                                                                                                                            |
| `spotify_resolved.items.IDX.artists`           | List (Dict)         | Associated Artists(s)                                                                                                                                |
| `spotify_resolved.items.IDX.artists.IDX2.name` | String              | Artist Name of artist at index IDX2                                                                                                                  |
| `spotify_resolved.items.IDX.artists.IDX2.name` | URI                 | Artist URI                                                                                                                                           |
| `spotify_resolved.artists.IDX.uri`             | String              | Artist URI on Spotify                                                                                                                                |
| `raw_title`                                    | String              | Raw title of the submission                                                                                                                          |
| `title`                                        | String              | Cleaned title of the submission                                                                                                                      |
| `raw_text`                                     | String              | Raw text of the submission                                                                                                                           |
| `text`                                         | String              | Cleaned text of the submission                                                                                                                       |
| `query_types`                                  | List (String)       | Type of query (can be multiple): `descriptive`, `user_created`, `extant_media`                                                                       |
| `split`                                        | String              | Split (`train`, `val`, `test`) used in the original experimentation. This value is `null` if the query wasn't used during benchmarking               |
| `annotations`                                  | List (Dict)         | Annotations per sentence. This value is `null` if the submission wasn't annotated.                                                                   |
| `annotations.IDX.id`                           | String              | ID of annotation at index IDX. Format is either `title_<sentence number>` (sentence was in title) or `text_<sentence number>` (sentence was in text) |
| `annotations.IDX.text`                         | String              | Sentence text                                                                                                                                        |
| `annotations.IDX.labels`                       | List (String)       | Set of labels associated with the sentence. See Table 1 in the paper for possible values and their descriptions.                                     |
| `reformulations`                               | Dict                | Reformulations. `null` if query wasn't used during benchmarking                                                                                      |
| `reformulations.keywords`                      | String              | List of keywords generated by Yake                                                                                                                   |
| `reformulations.reform_<N>`                    | String              | Generated reformulation up to `N` (= 10, 25, or 50) words (see paper)                                                                                |
| `reformuations.reform`                         | String              | Generated reformulation (without N constraint)                                                                                                       |



<a name="example-document"></a><details><summary>Click here to view example document</summary>

```json
{
  "id": "8sw82n",
  "wasabi_2.0_id": "5714dec425ac0d8aee38d04b",
  "wasabi_isrc": "USUM71506251",
  "annotations": [
    {
      "id": "title_0",
      "text": "pop song about being at the club but wanting to be somewhere else",
      "labels": [
        "Genre",
        "Story/Lyric Description"
      ]
    },
    {
      "id": "text_0",
      "text": "It's a recent pop song.",
      "labels": [
        "Genre",
        "Time Period / Recency"
      ]
    },
    {
      "id": "text_1",
      "text": "Maybe like 2 years old or something.",
      "labels": [
        "Uncertainty",
        "Time Period / Recency"
      ]
    },
    {
      "id": "text_2",
      "text": "Female singer.",
      "labels": [
        "Artist Description"
      ]
    },
    {
      "id": "text_3",
      "text": "I don't know the lyrics at all, but the basic gist of the song is about someone being at a club or party, and they're faking it, but in their mind they wish they were somewhere else.",
      "labels": [
        "Story/Lyric Description"
      ]
    },
    {
      "id": "text_4",
      "text": "I think the voice maybe sounds a bit like Halsey.",
      "labels": [
        "Vocals",
        "Relative Comparison",
        "Uncertainty"
      ]
    }
  ],
  "query_types": [
    "descriptive"
  ],
  "split": "train",
  "reformulations": {
    "keywords": "pop song, club but wanting",
    "reform_10": "Female pop song, Halsey-like, club/party, faking it.",
    "reform_25": "Pop song from the last two years, sung by a female artist with a Halsey-like voice, describing a person pretending to enjoy a club or party when they'd rather be somewhere else.",
    "reform_50": ".\n\nA recent pop song (2 years old or less) sung by a female artist, reminiscent of Halsey, about a person at a club or party faking enjoyment when they would rather be somewhere else.",
    "reform": "Recent pop song with female singer, sound like Halsey, about faking at a club or party."
  },
  "text": "It's a recent pop song. Maybe like 2 years old or something. Female singer.. . . I don't know the lyrics at all, but the basic gist of the song is about someone being at a club or party, and they're faking it, but in their mind they wish they were somewhere else.. . . I think the voice maybe sounds a bit like Halsey.",
  "raw_title": "[TOMT][song] pop song about being at the club but wanting to be somewhere else",
  "raw_text": "It's a recent pop song. Maybe like 2 years old or something. Female singer.\n\n\nI don't know the lyrics at all, but the basic gist of the song is about someone being at a club or party, and they're faking it, but in their mind they wish they were somewhere else.\n\n\nI think the voice maybe sounds a bit like Halsey.",
  "title": "pop song about being at the club but wanting to be somewhere else",
  "spotify_resolved": {
    "title": "Here",
    "items": [
      {
        "url": "https://open.spotify.com/track/5zUQZjVB6bfewBXWqsP9PY",
        "isrc": [
          "USUM71506251"
        ],
        "uri": "spotify:track:5zUQZjVB6bfewBXWqsP9PY",
        "album": {
          "name": "Know-It-All",
          "uri": "spotify:album:7HnbhIDKXIBhMR4EPGuMgu"
        },
        "artists": [
          {
            "name": "Alessia Cara",
            "uri": "spotify:artist:2wUjUUtkb5lvLKcGKsKqsR"
          }
        ]
      }
    ]
  }
}
```
