# The Podcast ActivityStream

> Version 1.0 by Yassine Doghri - 2021.04.15

The document aims to explain through examples and namespace definition how the existing RSS specification could be interfaced to [ActivityPub](https://www.w3.org/TR/activitypub/).

This is meant as a complementary work to the existing [RSS podcast namespace specification](https://github.com/Podcastindex-org/podcast-namespace) whilst unlocking features offered by the ActivityPub protocol.

## Context

A Podcast show is essentially constituted of two entities. In the RSS specification, these are placed under the `<channel>` and `<item>` tags. The `<channel>`, referring to the Podcast, may include multiple `<item>` tags which are the Podcast episodes.

[The ActivityPub protocol](https://www.w3.org/TR/activitypub) is a decentralized social networking protocol based upon the [ActivityStreams 2.0](https://www.w3.org/TR/activitystreams-core/) data format. This offers a base vocabulary for social interactions between decentralized servers and allows us to extend it for podcasting.

The syntax for defining the ActivityStreams 2.0 data format is called [JSON-LD](https://json-ld.org/), a method of encoding linked data using JSON.

Just as the RSS specification, the **Podcast ActivityStream** defines two entities:

- [Podcast Actor](#the-podcast-object)
- [PodcastEpisode Object](#the-podcastepisode-object).

## The Podcast Actor

The Podcast Actor extends the [Actor Object](https://www.w3.org/TR/activitypub/#actors) from ActivityPub to include specific podcast attributes.

Here is an example of a Podcast Actor:

```json
{
  "@context": [
    "https://www.w3.org/ns/activitystreams",
    "https://w3id.org/security/v1",
    "https://github.com/Podcastindex-org/activitypub-spec-work/blob/main/docs/1.0.md"
  ],
  "to": ["https://www.w3.org/ns/activitystreams#Public"],
  "id": "https://podcast.demo/podcasts/DemoPodcast",
  "type": "Podcast",
  "rss": "https://podcast.demo/podcasts/DemoPodcast/feed.xml",
  "name": "The Demo Podcast",
  "preferredUsername": "DemoPodcast",
  "summary": "<p>This is a demonstration of the activitypub protocol applied to Podcasts!</p>",
  "inbox": "https://podcast.demo/podcasts/DemoPodcast/inbox",
  "outbox": "https://podcast.demo/podcasts/DemoPodcast/outbox",
  "followers": "https://podcast.demo/podcasts/DemoPodcast/followers",
  "following": "https://podcast.demo/podcasts/DemoPodcast/following",
  "episodes": "https://podcast.demo/podcasts/DemoPodcast/episodes",
  "url": "https://podcast.demo/podcasts/DemoPodcast",
  "image": {
    "type": "Image",
    "mediaType": "image/jpeg",
    "url": "https://podcast.demo/media/podcasts/DemoPodcast/cover.jpg"
  },
  "icon": {
    "type": "Image",
    "mediaType": "image/jpeg",
    "url": "https://podcast.demo/media/podcasts/DemoPodcast/avatar.jpg"
  },
  "language": "en",
  "category": "Fiction > Science Fiction",
  "explicit": false,
  "publisher": {
    "@type": "Organization",
    "name": "John Doe Corp.",
    "email": "contact@johndoe.demo"
  },
  "author": {
    "@type": "Person",
    "name": "Jane Doe",
    "email": "jane.doe@podcast.demo"
  },
  "owner": {
    "@type": "Person",
    "name": "John Doe",
    "email": "john.doe@podcast.demo"
  },
  "persons": "https://podcast.demo/podcasts/DemoPodcast/persons",
  "location": {
    "@type": "Place",
    "geo": {
      "@type": "GeoCoordinates",
      "latitude": "48.8566969",
      "longitude": "2.3514616"
    },
    "name": "Paris, France"
  },
  "trailer": "https://podcast.demo/podcasts/DemoPodcast/trailer",
  "copyrightHolder": {
    "@type": "Person",
    "name": "Jane Doe",
    "sameAs": "https://en.wikipedia.org/wiki/jane_doe"
  },
  "copyrightNotice": "(CC BY-ND 4.0)",
  "copyrightYear": 2021,
  "discoverable": false,
  "complete": false,
  "locked": true,
  "license": "https://creativecommons.org/licenses/by-nd/4.0/",
  "value": {
    "type": "Value",
    "id": "https://podcast.demo/podcasts/DemoPodcast/value",
    "method": "keysend",
    "suggested": "0.00000005000",
    "valueRecipients": "https://podcast.demo/podcasts/DemoPodcast/value/recipients"
  },
  "publicKey": {
    "id": "https://podcast.demo/podcasts/DemoPodcast#main-key",
    "owner": "https://podcast.demo/podcasts/DemoPodcast",
    "publicKeyPem": "-----BEGIN PUBLIC KEY----- ... -----END PUBLIC KEY-----"
  }
}
```

### Notes about the attributes

- `publisher` corresponds to the `author` tag in the [itunes RSS spec](https://help.apple.com/itc/podcasts_connect/#/itcb54353390).
- `discoverable` defines whether or not the podcast (or episode) should be visible on other platforms. Corresponds to the `block` tag in the itunes RSS spec.
- `complete` whether or not the podcast show is over (no more new episodes to be expected).
- `movedTo` corresponds to the `new-feed-url` tag in the rss feed. Adopted by Mastodon though not an officially.

## The PodcastEpisode Object

The PodcastEpisode Object extends the base [Object type](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-object) from ActivityPub to include all attributes specific to a podcast episode. It also includes an extended [Audio Object](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-audio) for the podcast episode's audio file.

Here is an example of a PodcastEpisode Object:

```json
{
  "@context": [
    "https://www.w3.org/ns/activitystreams",
    "https://github.com/Podcastindex-org/activitypub-spec-work/blob/main/docs/1.0.md"
  ],
  "type": "PodcastEpisode",
  "id": "https://podcast.demo/podcasts/DemoPodcast/episodes/example-episode",
  "attributedTo": "https://podcast.demo/podcasts/DemoPodcast",
  "to": ["https://www.w3.org/ns/activitystreams#Public"],
  "cc": ["https://podcast.demo/podcasts/DemoPodcast/followers"],
  "name": "An Example PodcastEpisode Object",
  "description": {
    "type": "Note",
    "mediaType": "text/markdown",
    "content": "Here is the description for the **demo episode**!",
    "contentMap": {
      "en": "<p>Here is the description for the <strong>demo episode</strong>!</p>",
      "fr": "<p>Voici la description pour la <strong>démo de l’épisode</strong> !</p>"
    }
  },
  "image": {
    "type": "Image",
    "mediaType": "image/jpeg",
    "url": "https://podcast.demo/media/example-episode_cover.jpg"
  },
  "audio": {
    "id": "https://podcast.demo/podcasts/activitypub/episodes/example-episode.mp3",
    "type": "Audio",
    "name": "An Example PodcastEpisode Object",
    "size": 1962804,
    "bitrate": 320000,
    "duration": 42,
    "url": {
      "href": "https://podcast.demo/media/example-episode.mp3",
      "type": "Link",
      "mediaType": "audio/mpeg"
    },
    "caption": "https://podcast.demo/media/example-episode/caption",
    "transcript": "https://podcast.demo/media/example-episode/transcript",
    "chapters": "https://podcast.demo/media/example-episode/chapters"
  },
  "partOfSeason": "https://podcast.demo/podcasts/DemoPodcast/seasons/1",
  "episodeNumber": 1,
  "explicit": false,
  "location": {
    "@type": "Place",
    "geo": {
      "@type": "GeoCoordinates",
      "latitude": "48.8566969",
      "longitude": "2.3514616"
    },
    "name": "Paris, France"
  },
  "discoverable": true,
  "replies": "https://podcast.demo/podcasts/DemoPodcast/episodes/example-episode/replies",
  "published": "2021-04-15T18:00:00Z"
}
```

## The JSON-LD namespace definition

The [ActivityStreams base vocabulary](https://www.w3.org/TR/activitystreams-vocabulary/) was extended to create [The Podcast JSON-LD namespace](./podcast-jsonld-namespace.md)

## Going further

The JSON-LD syntax offers a wide range of features that go beyond the RSS file: direct social interaction, pagination, translations, etc.

You can check out the [examples folder](./examples) to get a glimpse into the possibilities of ActivityPub.

---

This work has been inspired and made possible with the amazing free and open-source projects on the internet:

- [Podcastindex-org/podcast-namespace](https://github.com/Podcastindex-org/podcast-namespace)
- [ActivityPub](https://www.w3.org/TR/activitypub)
- [Schema.org](https://schema.org/)
- [Mastodon](https://docs.joinmastodon.org/spec/activitypub/)
- [Funkwhale](https://docs.funkwhale.audio/federation/index.html)
- ...
