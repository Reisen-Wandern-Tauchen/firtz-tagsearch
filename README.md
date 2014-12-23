# firtz-tagsearch
*tag- and keyword-search for the firtz podcast publisher*

## Deutsch
Es handelt sich hier um eine Erweiterung für den firtz podcast publisher.
Diese besteht darin, dem firtz eine Schlagwort-Suche innerhalb aller Posts zu ermöglichen. Die Suchroutine übernimmt ein Schlagwort bzw. eine Suchphrase und führt damit eine Suche innerhalb der Schlüsselwörter (keywords) in jeder Episode durch.
Es wird nicht der Artikel-Text der Episode durchsucht sondern nur die definierten Schlüsselwörter! (diese Funktion wird eventuell irgendwann ergänzt...)

### Installation
Kopiere zunächst den Ordner `/ext/tags` mit allen darin enthaltenen Dateien in Deine firtz-Installation.

Anschließend musst Du noch die entsprechenden Einträge in den Wörterbüchern des firtz vornehmen.
Wechsle dazu in den Ordner `/dict`. Hier findest Du nun zwei Dateien, welche Du beide bearbeiten musst.  
In die Datei `/dict/de.php` füge folge Definition ein:
```
'dict_tagsearch' => 'Schlagwort-Suche',
```

In die Datei `/dict/en.php` füge folge Definition ein:
```
'dict_tagsearch' => 'Tag-Search',
```

Um in jeder Episode unterhalb des Artikels bzw. Players automatisch eine Schlagwort-Liste mit den entsprechenden Link zur Suchabfrage anzuzeigen suche in Deiner *template/site.html* nach folgendem Codeblock
```
<div> 
	<repeat group="{{glob(@templatepath.'/episode/*.html')}}" value="{{@template}}"> 
		<include href="{{'episode/'.basename(@template)}}"/> 
	</repeat> 
</div> 
```
und füge unmittelbar davor diesen Code ein:
```html
<check if="{{trim(@item.keywords)!=''}}"> 
	<div class="well">Tags:  
		<repeat group="{{(explode(',', @item.keywords))}}" value="{{@keyword}}"><a href="{{@BASEURL}}{{@feedattr.slug}}/tags/{{@keyword}}">{{@keyword}}</a> </repeat> 
	</div> 
</check>
```

### Verwendung
Verwende folgenden Aufruf um eine Suche zu starten: `http://deine.podcast.url/podcastname/tags/SCHLUESSELWORT`  
Als Ergebnis erhältst Du eine Liste aller Episoden, welche mit dem gesuchten Schlagwort / Phrase versehen sind. Die Liste ähnelt der, die Du aus dem Podcast-Archiv kennst.

## english version
This is an extension to the firtz podcast publisher.
It will add a possibility to run a keyword-search over all posts. The search-routine takes a single keyword or a (exact) phrase and performs a search in the defined keywords of every article.
It does not perform a search in the article-text! (this feature will maybe added some day...)

### install
Copy the folder `/ext/tags` with all files to your firtz-installation.

After that you have to insert the corresponding entries into the dictionaries.
Therefore go to the folder `/dict`. There you'll find two files you have to edit.  
In `/dict/de.php` instert:
```
'dict_tagsearch' => 'Schlagwort-Suche',
```

In `/dict/en.php` insert:
```
'dict_tagsearch' => 'Tag-Search',
```

To automatically add a keyword-list with corresponding search-links beneath the article / player in every episode look for something like
```
<div> 
	<repeat group="{{glob(@templatepath.'/episode/*.html')}}" value="{{@template}}"> 
		<include href="{{'episode/'.basename(@template)}}"/> 
	</repeat> 
</div> 
```
inside your *template/site.html* and add this codeblock just right before:
```html
<check if="{{trim(@item.keywords)!=''}}"> 
	<div class="well">Tags:  
		<repeat group="{{(explode(',', @item.keywords))}}" value="{{@keyword}}"><a href="{{@BASEURL}}{{@feedattr.slug}}/tags/{{@keyword}}">{{@keyword}}</a> </repeat> 
	</div> 
</check>
```

### use
To perform the search use: `http://your.podcast.url/podcast-name/tags/KEYWORD`  
The result is a list of all episodes containing the keyword / phrase. This list is similar to this you know of the podcast-archive.
