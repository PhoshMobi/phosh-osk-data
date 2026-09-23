project(
  'phosh-osk-data',
  version: '0.58.0',
  meson_version: '>= 1.1.0',
)

prefix = get_option('prefix')
bin = meson.project_name() + '-packager'
datadir = prefix / get_option('datadir')

install_data(
  bin,
  install_dir: prefix / get_option('bindir'),
)

flake8 = find_program('flake8')
scripts = [bin, 'pod-db-from-wiki-dump']
foreach script : scripts
  test(
    'flake8',
    flake8,
    args: ['--format=pylint', script],
    workdir: meson.global_source_root(),
  )
endforeach

subdir('doc')
