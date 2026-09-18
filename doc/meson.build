rst2man = find_program('rst2man')

custom_target(
  'manpage',
  command: [rst2man, '--syntax-highlight=none', '@INPUT@'],
  capture: true,
  input: f'@bin@.rst',
  output: f'@bin@.1',
  install_dir: datadir / 'man' / 'man1',
  install: true,
  build_by_default: true,
)
