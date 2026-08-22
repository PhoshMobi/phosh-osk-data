# phosh osk data

Scripts to build word prediction data for [phosh-osk-stevia][] (formerly
known as phosh-osk-stub) and other presage based completers. The aim here is to
have models that are distributable without licensing issues and using modern
language so we're using Wikipedia dumps.

## Building your own dictionaries based in Wikipedia data

Get a host with disk space (~40G), more cores make the first steps
(extraction and parsing into sentences significantly faster.

You can then provision it with the provided ansible playbook on your
cloud provider of choice:

```sh
   ansible-playbook -v -i "${BUILDER}", -u root  builder/setup.yml
```

`${BUILDER}` is the IP or hostname of the host to provision.

Once there get the Wikipedia dump:

```sh
ssh ${BUILDER}
mkdir output/
cd output/
export POS_LANG=es
wget "https://dumps.wikimedia.org/${POS_LANG}wiki/latest/${POS_LANG}wiki-latest-pages-articles.xml.bz2"
```

Import some nltk data:

```sh
python3 -c "import nltk; nltk.download('punkt')"
```

Process the dump

```sh
./pod-db-from-wiki-dump --processes "$(nproc)" --language "${POS_LANG}" --dump "output/${POS_LANG}wiki-latest-pages-articles.xml.bz2" --output  "output/${POS_LANG}"
```

You'll then get a database usable by presage based completers in `output/${POS_LANG}/database_${POS_LANG}.db`.

This happens in steps so should a step fail you can skip it in subsequent runs.
See the `--skip-*` options. The extract and parsing steps happen in parallel
and can be spread over multiple cores (default `8`).

## Installing the data

See the [phosh-data-packager manpage](doc/phosh-osk-data-packager.rst).

## Available Languages

For a list of available languages see <https://data.phosh.mobi/osk-data/latest/presage/>.

## Related projects

- presage: <http://presage.sourceforge.net/>
- sfos presage databases: <https://github.com/sailfish-keyboard/presage-database>
- stevia on screen keyboard: <https://gitlab.gnome.org/World/Phosh/stevia>

## Getting in Touch

- Issue tracker: <https://gitlab.gnome.org/World/Phosh/phosh-osk-data/issues/>
- Matrix: <https://matrix.to/#/#phosh:phosh.mobi>

[phosh-osk-stevia]: https://gitlab.gnome.org/World/Phosh/stevia
