# The Podcast JSON-LD namespace definition

> Version 1.0 by Yassine Doghri - 2021.04.15

To retain maximum compatibility and avoid reinventing the wheel, most of the attributes are defined as being a subset of existing objects in the [ActivityStreams 2.0 data format](https://www.w3.org/TR/activitystreams-vocabulary/) and [Schema.org](https://schema.org/).
For more information, see [Namespace Reference](#namespace-references).

```json
{
  "@context": {
    "id": "@id",
    "type": "@type",
    "as": "https://www.w3.org/ns/activitystreams#",
    "schema": "http://schema.org#",
    "podcast": "https://podcast.org/ns#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "Podcast": "podcast:Podcast",
    "PodcastEpisode": "podcast:PodcastEpisode",
    "publisher": "schema:publisher",
    "author": "schema:author",
    "owner": "schema:Person",
    "category": "schema:category",
    "language": "schema:inLanguage",
    "location": "schema:location",
    "license": "schema:license",
    "explicit": "podcast:explicit",
    "discoverable": "podcast:discoverable",
    "complete": "podcast:complete",
    "locked": "podcast:locked",
    "copyrightHolder": "schema:copyrightHolder",
    "copyrightNotice": "schema:copyrightNotice",
    "copyrightYear": "schema:copyrightYear",
    "description": "as:Note",
    "partOfPodcastEpisode": "podcast:partOfPodcastEpisode",
    "episodes": {
      "@id": "podcast:episodes",
      "@type": "@id"
    },
    "persons": {
      "@id": "podcast:persons",
      "@type": "@id"
    },
    "movedTo": {
      "@id": "as:movedTo",
      "@type": "@id"
    },
    "audio": {
      "@id": "as:Audio",
      "@type": "@id"
    },
    "partOfSeason": {
      "@id": "schema:PodcastSeason",
      "@type": "@id"
    },
    "trailer": {
      "@id": "podcast:PodcastEpisode",
      "@type": "@id"
    }
  }
}
```

## Namespace References

### ActivityStreams extensions

- [Note object](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-note)
- [Audio object](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-audio)
- [movedTo](https://www.w3.org/ns/activitystreams#movedTo)

### Schema.org extensions

- [PodcastEpisode](https://schema.org/PodcastEpisode)
- [PodcastSeason](https://schema.org/PodcastSeason)
- [publisher](https://schema.org/publisher)
- [person](https://schema.org/Person)
- [category](https://schema.org/Category)
- [inLanguage](https://schema.org/inLanguage)
- [location](https://schema.org/location)
- [license](https://schema.org/license)
- [copyrightHolder](https://schema.org/copyrightHolder)
- [copyrightNotice](https://schema.org/copyrightNotice)
- [copyrightYear](https://schema.org/copyrightYear)
- [AudioObject](https://schema.org/AudioObject)
