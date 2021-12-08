# script.module.streamlink.base

Streamlink library packed for Kodi: [Upstream link](https://github.com/streamlink/streamlink)

You can install it from [repository.Syco](https://syco.github.io/Cool-Stuff/repo/)

## Extracting streams
### The simplest use of the Streamlink API looks like this:

    import streamlink
    streams = streamlink.streams("https://www.youtube.com/watch?v=XIMLoLxmTDw")
    url = streams['best'].to_url()

Where url can be passed into the player:

    xbmc.Player().play(url)


If no plugin for the URL is found, a **NoPluginError** will be raised.

If an error occurs while fetching streams, a **PluginError** will be raised.

### Session based usage, which allows plugin options to be passed

    import streamlink.session

    def resolve(url, quality='best'):

        try:

            session = streamlink.session.Streamlink()
            plugin = session.resolve_url(url)
            streams = plugin.get_streams()
            playable_link = streams[quality].to_url()

            return playable_link

        except:

            pass

### build instructions
```bash
docker run --net host -it --rm -v ${PWD}:/root:rw python:3.7 /bin/bash
bind 'set enable-bracketed-paste off'
cd ~
rm -Rf lib
pip3.7 install --exists-action=i --prefix=lib streamlink
rm -Rf lib/bin lib/share
mv lib/lib/python3.7/site-packages/* lib/
rm -Rf lib/lib
rm -Rf lib/*.dist-info
exit

sudo rm .bash_history
sudo chown -R $(id -u).$(id -g) .
find -type d -name __pycache__ | xargs -r rm -Rf


####################################################################
sed -i '/__version__/d' lib/pycountry/__init__.py

####################################################################
rm -Rf lib/lxml

## from xml.etree import ElementTree as ET

vim lib/streamlink/plugin/api/validate.py
# %sno/Element/ET.Element/gc
# %sno/iselement/ET.iselement/gc

vim lib/streamlink/plugins/radiko.py
# %sno/XML/ET.XML/gc

vim lib/streamlink/utils/parse.py
# %sno/HTML/ET.HTML/gc
# %sno/XML/ET.XML/gc
# %sno/lxml.etree.ET./ET./gc


grep --exclude-dir=.svn --exclude-dir=.git -RIls -m1 lxml

####################################################################

```
