# DMX CSV Importer

Note: CSV importing is pretty funny with the new value DMX integration. Sadly, I don't understand it fully yet (or found an issue). 

A simple CSV importer to import and update flat topic compositions in [DMX 5.0-beta-7-SNAPSHOT](https://github.com/jri/deepamehta).

Limitations:

 * delimiter: ```|``` (default)
 * data type: Text

## Usage

You need to create yourself a `File` topic manually first. This can be done through issueing a `GET` request to the FileService endpoint, e.g.:

`http://localhost:8080/files/file/notes.csv`


## Download

You can find the recommended (not-SNAPSHOT) versions of this plugin in its directory at [https://download.dmx.systems/plugins/](https://download.dmx.systems/plugins/).

## Requirements

 * [DMX](https://github.com/jri/deepamehta) 5.0-beta-7-SNAPSHOT+
 * Write access to `dmx.filerepo.path` (see DM4 `config.properties` file)

## Usage

The plugin adds an *Import CSV* command to all `Topic Type`-Topics, which are those with a blue square as an icon.


### Import some topics from a CSV file

To create some *Note* topics use a CSV file (a simple text-file) structured like the following:

```
csv.example | dmx.notes.title | dmx.notes.text
one         | check this      | with content
two         | check this too  | and with another content
```

You could then upload this file through using the *Import CSV* command of the *Note* topic type. For each line, beginning at the second, there will be a *Note* created in your DeepaMehta 4 installation.

Alternatively: A CSV file to import some *Web Resource* topics would need its contents structured like the following:

```
deep.web | dmx.webbrowser.url        | dmx.webbrowser.web_resource_description
site     | http://www.deepamehta.de  | <h1>DeepaMehta</h1><p class="slogan">Cope With Complexity</p>
demo     | http://demo.deepamehta.de | <h1>Demo Server</h1><p>try it now</p>
ci       | http://ci.deepamehta.de   | <h1>Continuous Integration</h1><p>fresh nightly builds</p>
```


### Update existing topics

To update all instances of a topic type just import the modified CSV file again,
but be aware of these rules:

 * existing topic is updated by a URI match
 * row without a matching topic URI creates a new topic instance
 * existing topic instance with a type URI and no actual row match is deleted


### CSV Format Description

 * topic URI prefix as the first entry (row: 0, col: 0)
 * all direct child topics are the remaining header columns
 * one topic per row with topic URI suffix in the first column

### Authors

(C) Malte Reißig 2013-2020
(C) Danny Graf 2013-2015
