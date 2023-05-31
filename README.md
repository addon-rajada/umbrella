# Umbrella

[Umbrella](https://github.com/umbrellaplug/umbrellaplug.github.io) com alterações para funcionamento com Elementum ao invés de serviços Debrid

---

## Idioma da API

Nos arquivos:

- movies.py
- tvshows.py
- cleangenre.py
- control.py

trocar os códigos **pt** por **pt-BR**

---

## Menu de Contexto

Desativar todos pelo addon.xml ou no código (comentar chamadas addContextMenuItems)

---

## Settings.xml

- page.item.limit 40
- search.page.limit 40
- api.language Portuguese
- mpa.country Brazil
- enable.fanarttv false
- tmdb.imageResolutions 0 (low) 3 (original)
- navigation ...
- navigation(movies) ...
- navigation(tvshows) ...

---

## Addon.xml

Alterar name, provider-name, summary, description e news

---

## Items URL

Nos arquivos:

- collections.py, função movieDirectory
- tvshows.py, função tvshowDirectory (não precisa se tiver o menu de contexto)
- episodes.py, função episodeDirectory
- movies.py, função movieDirectory

trocar a URL padrão dos itens pela URL do elementum:

```python
url = "plugin://plugin.video.elementum" + quote("/context/media/%s/%s/play" % ("movie", ("%s %s" % (title, year))))
```

em sysurl, usar quote() ao invés de quote_plus(). necessário o import

usar url modificada na chamada **control.addItem**

---

No arquivo tvshows.py, adicionar os comandos para item

```python
item.setProperty('IsPlayable', 'true')
item.setProperty('ForceResolvePlugin', 'true')
control.addItem(handle=syshandle, url=url, listitem=item, isFolder=False)
```

---

No arquivo router.py

Nas actions **play_Item** e **play**, comentar tudo

---

## View Mode

Nos arquivos:

- collections.py
- movies.py
- tvshows.py

Trocar opção de view na chamada **views.setView** para estuary e confluence

```
50 List
51 Poster
52 IconWall
53 Shift
54 InfoWall
55 WideList
500 Wall
501 Banner
502 FanArt
503 NowPlaying
```

---

## Skins

remover pasta /resources/skins/ na geração do arquivo zip
