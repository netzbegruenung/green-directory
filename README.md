# Green Directory

Structured data repository of Green Party organisations

## Goals

- Enable applications in need of structured data regarding
  Green party organizations

- Provide high quality, well maintained structured data

- Allow for an open and transparent data maintenance workflow
  based on Github pull requests.

## Help Wanted

This project needs help with:

- Structured data imports: As soon as a schema is defined initially,
  we need help with importing data. Pull requests welcome!

Please also look at the [issues](https://github.com/netzbegruenung/green-directory/issues)
for anything tagged with `help wanted`.

When in doubt, please file an issue to ask a question or report
a feature wish.

## Data Structure

- YAML is used as a source format.

- We try to avoid as much extra markup as possible (quotes, brackets)

- We have a folder structure that helps humans to find relevant files,
  but which should not be read in a semantical fashion. The folder hierarchy
  can vary from country to country and from locality to locality.
  Likewise, data file names have no meaning.

- YAML files have the ending `.yaml`.

- All data files are lists of entries (starting with a `---` line). Every file ends with a new line character.

- The schema definition (attributes and permitted values) depends on the
  type of entry. See below for details.

## Attributes

If not indicated otherwise, all attributes are of the type `String`.

- `type` (mandatory): Type of the entry. Possible values:
  - `PARTY`: A political party, usually active in the entire country.
  - `REGIONAL_CHAPTER` - a subdivision of an organisation, usually
    assigned to a local territory.
  - `COMMITTEE`: A not locally assigned sub-group of a party
    organisation.
  - `YOUTH_ORGANIZATION`: A youth organization which is normally associated
    with a party.
  - `SUB_ORGANIZATION`: Some other sub-organization of a party.
  - `PERSON`: An individual with an important function (e.g. Member of Parliament).
  - `PARLIAMENTARY_GROUP` : A parliamentary group (german: Fraktion) of a political party in a city council or parliament.

- `level` (mandatory, except for Members of the European Parliament). A sub-classification of an entry with type `REGIONAL_CHAPTER`. Possible values:
  - `DE:BUNDESVERBAND` 
  - `DE:LANDESVERBAND`: A chapter belonging to a federal state in Germany. The
    "Land" (also known as "Bundesland") is the primary territorial subdivision
    of the Federal Republic of Germany. See https://en.wikipedia.org/wiki/States_of_Germany
  - `DE:BEZIRKSVERBAND`: A chapter belonging to more than one district. Mostly used in southern Germany. See https://de.wikipedia.org/wiki/H%C3%B6herer_Kommunalverband
  - `DE:KREISVERBAND`: A "Kreisverband" in Germany (DE), which is a regional
    chapter of the party belonging to a "Kreis", which is a kind of district.
    A "Kreis" is, in most German federal states, the primary administrative
    subdivision. See https://en.wikipedia.org/wiki/Districts_of_Germany
  - `DE:REGIONALVERBAND`: A chapter which is smaller than a "Kreisverband", but has (or could have) sub-chapters.
  - `DE:ORTSVERBAND`: A chapter belonging to a town or a part of a city

- `country` (mandatory, except for Members of the European Parliament). Two-letter country code of the country the entry is active in, according to ISO 3166-1 alpha-2. Possible value:
  - `DE` for Germany

- `state` (mandatory for every entry below "DE:BUNDESVERBAND"). Federal state or province the entry is active in. Please use the word that is common in the country, not the english translation. Examples:
  - `Bayern` for Bavaria
  - `Nordrhein-Westfalen` for North Rhine-Westphalia

- `district` OR `region` OR `city` (mandatory for every entry below "DE:LANDESVERBAND"). district, region or city the entry is active in. Examples:
  - `district` for a "Kreisverband" (even if it is a "kreisfreie Stadt")
  - `region` for a "Regionalverband" or "Bezirksverband"
  - `city` for a "Ortsverband" (even if it is only a part of a city)

- `urls` (mandatory). Contians one or more URLs for websites, social media account or other ressources. URLs are of the type `Array`
  - An URLs-Array has two parts:
    - `type` defines the following url. Often used (This list may be incomplete):
      - `WEBSITE` for the website of the entry
      - `FACEBOOK` for the Facebook-page of the entry
      - `TWITTER` for the Twitter-page of the entry
      - `INSTAGRAM` for the Instagram-page of the entry
      - `MASTODON` for the Mastodon-page of the entry
      - `YOUTUBE` for the Youtube-page of the entry
      - `WIKIDATA` for the url to the Wikidata-object. (The corresponding url will look like this: `https://www.wikidata.org/wiki/Q49766`)
    - `url` is a unique website adress. Must start with `https://` or `http://`. If possible, use `https://` and do not use `www.`. If the type is "WEBSITE", it should end with the character `/`.

- `emails` (optional). Contains usually one email adress. Emails are of the type `Array`
  - An emails-Array has one part:
    - `address` defines the email contact information

For entrys of the type "Person", there are the following attributes (additionally to the above mentioned).

- `name` (mandatory): Name the person is commonly known by, usually consisting of given and family name.

- `given_name` (mandatory): The name usually given to the person by their parents. See https://schema.org/givenName

- `family_name` (mandatory): The name usually also carried by other family members. See https://schema.org/familyName


## Contributing

Pull requests with data corrections and contributions are welcome.

Please validate your data before submitting a pull request. To do this, run
the following command in the terminal:

```
make validate
```

If the command runs without error notice, everything is fine.
