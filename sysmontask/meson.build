
gnome = import('gnome')
i18n   = import('i18n')
python = import('python')

py_installation = python.find_installation('python3')
python_version = py_installation.language_version()
python_version_req = '>=3.8'
if not py_installation.found()
    error('No valid python3 binary found')
endif
if not python_version.version_compare(python_version_req)
  error('Requires Python @0@, @1@ found.'.format(python_version_req, python_version))
endif

gettext_package = meson.project_name()
localedir = get_option('prefix') / get_option('localedir')
pythondir = py_installation.get_path('purelib')
datadir = get_option('prefix') / get_option('datadir')
pkgdatadir = datadir / meson.project_name()
podir = meson.source_root() / 'po'

conf = configuration_data()
conf.set('PYTHON_DIR', pythondir)

configure_file(
  input: 'sysmontask.py',
  output: 'sysmontask',
  configuration: conf,
  install: true,
  install_dir: get_option('bindir')
)

local_config = configuration_data()
local_config.set('PYTHON_DIR', meson.source_root())
local_config.set('LOCAL_BUILD', 'True')


install_subdir(
  '../sysmontask',
  install_dir: py_installation.get_install_dir()
)

install_subdir(
	'../glade_files',
	install_dir: join_paths(get_option('datadir'), 'sysmontask')
)


